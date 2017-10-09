# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a><span data-ttu-id="4390d-101">Preguntas más frecuentes sobre los discos de máquina virtual de IaaS de Azure y los discos premium administrados y no administrados</span><span class="sxs-lookup"><span data-stu-id="4390d-101">Frequently asked questions about Azure IaaS VM disks and managed and unmanaged premium disks</span></span>

<span data-ttu-id="4390d-102">En este artículo se responden algunas de las preguntas más frecuentes acerca de Azure Managed Disks y Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="4390d-102">This article answers some frequently asked questions about Azure Managed Disks and Azure Premium Storage.</span></span>

## <a name="managed-disks"></a><span data-ttu-id="4390d-103">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="4390d-103">Managed Disks</span></span>

<span data-ttu-id="4390d-104">**¿Qué es Azure Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="4390d-104">**What is Azure Managed Disks?**</span></span>

<span data-ttu-id="4390d-105">Managed Disks es una característica que simplifica la administración de discos para máquinas virtuales de IaaS de Azure al controlar automáticamente la administración de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4390d-105">Managed Disks is a feature that simplifies disk management for Azure IaaS VMs by handling storage account management for you.</span></span> <span data-ttu-id="4390d-106">Para obtener más información, vea hello [información general de discos administrados](../articles/virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4390d-106">For more information, see hello [Managed Disks overview](../articles/virtual-machines/windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="4390d-107">**Si creo un disco administrado estándar a partir un disco duro virtual existente con 80 GB de tamaño, ¿cuánto me costará?**</span><span class="sxs-lookup"><span data-stu-id="4390d-107">**If I create a standard managed disk from an existing VHD that's 80 GB, how much will that cost me?**</span></span>

<span data-ttu-id="4390d-108">Un disco administrado estándar creado a partir de un VHD de 80 GB se trata como el tamaño de disco estándar disponible siguiente hello, que es un disco S10.</span><span class="sxs-lookup"><span data-stu-id="4390d-108">A standard managed disk created from an 80-GB VHD is treated as hello next available standard disk size, which is an S10 disk.</span></span> <span data-ttu-id="4390d-109">Se le cobrará correspondiente toohello S10 disco precios.</span><span class="sxs-lookup"><span data-stu-id="4390d-109">You're charged according toohello S10 disk pricing.</span></span> <span data-ttu-id="4390d-110">Para obtener más información, vea hello [página de precios](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="4390d-110">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="4390d-111">**¿Existen costes de transacción para los discos administrados estándar?**</span><span class="sxs-lookup"><span data-stu-id="4390d-111">**Are there any transaction costs for standard managed disks?**</span></span>

<span data-ttu-id="4390d-112">Sí.</span><span class="sxs-lookup"><span data-stu-id="4390d-112">Yes.</span></span> <span data-ttu-id="4390d-113">Sí, se le cobrará por cada transacción.</span><span class="sxs-lookup"><span data-stu-id="4390d-113">You're charged for each transaction.</span></span> <span data-ttu-id="4390d-114">Para obtener más información, vea hello [página de precios](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="4390d-114">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="4390d-115">**¿Para un disco administrado estándar, se me cobrarán de tamaño real de Hola de datos de hello en el disco de Hola o de hello aprovisionar capacidad de hello disco?**</span><span class="sxs-lookup"><span data-stu-id="4390d-115">**For a standard managed disk, will I be charged for hello actual size of hello data on hello disk or for hello provisioned capacity of hello disk?**</span></span>

<span data-ttu-id="4390d-116">Se le cobrará en función de la capacidad de hello aprovisionado del disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="4390d-116">You're charged based on hello provisioned capacity of hello disk.</span></span> <span data-ttu-id="4390d-117">Para obtener más información, vea hello [página de precios](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="4390d-117">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="4390d-118">**¿En qué se diferencian los precios de los discos administrados premium de los de los discos no administrados?**</span><span class="sxs-lookup"><span data-stu-id="4390d-118">**How is pricing of premium managed disks different from unmanaged disks?**</span></span>

<span data-ttu-id="4390d-119">Hola precios de discos premium administrado es Hola igual que los discos premium no administrado.</span><span class="sxs-lookup"><span data-stu-id="4390d-119">hello pricing of premium managed disks is hello same as unmanaged premium disks.</span></span>

<span data-ttu-id="4390d-120">**¿Puedo cambiar Hola almacenamiento tipo de cuenta (Standard o Premium) de Mis discos administrados?**</span><span class="sxs-lookup"><span data-stu-id="4390d-120">**Can I change hello storage account type (Standard or Premium) of my managed disks?**</span></span>

<span data-ttu-id="4390d-121">Sí.</span><span class="sxs-lookup"><span data-stu-id="4390d-121">Yes.</span></span> <span data-ttu-id="4390d-122">Puede cambiar el tipo de cuenta de almacenamiento de Hola de los discos administrados mediante Hola portal de Azure, PowerShell u Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="4390d-122">You can change hello storage account type of your managed disks by using hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="4390d-123">**¿Hay alguna manera que puedo copiar o exportar una cuenta de almacenamiento privado de disco administrado tooa?**</span><span class="sxs-lookup"><span data-stu-id="4390d-123">**Is there a way that I can copy or export a managed disk tooa private storage account?**</span></span>

<span data-ttu-id="4390d-124">Sí.</span><span class="sxs-lookup"><span data-stu-id="4390d-124">Yes.</span></span> <span data-ttu-id="4390d-125">Puede exportar los discos administrados mediante Hola portal de Azure, PowerShell u Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="4390d-125">You can export your managed disks by using hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="4390d-126">**¿Puedo usar un archivo de disco duro virtual en un toocreate de cuenta de almacenamiento de Azure un disco administrado con una suscripción diferente?**</span><span class="sxs-lookup"><span data-stu-id="4390d-126">**Can I use a VHD file in an Azure storage account toocreate a managed disk with a different subscription?**</span></span>

<span data-ttu-id="4390d-127">No.</span><span class="sxs-lookup"><span data-stu-id="4390d-127">No.</span></span>

<span data-ttu-id="4390d-128">**¿Puedo usar un archivo de disco duro virtual en un toocreate de cuenta de almacenamiento de Azure un disco administrado en una región distinta?**</span><span class="sxs-lookup"><span data-stu-id="4390d-128">**Can I use a VHD file in an Azure storage account toocreate a managed disk in a different region?**</span></span>

<span data-ttu-id="4390d-129">No.</span><span class="sxs-lookup"><span data-stu-id="4390d-129">No.</span></span>

<span data-ttu-id="4390d-130">**¿Hay alguna limitación de escala para los clientes que usen discos administrados?**</span><span class="sxs-lookup"><span data-stu-id="4390d-130">**Are there any scale limitations for customers that use managed disks?**</span></span>

<span data-ttu-id="4390d-131">Discos administrados elimina los límites de hello asociados con las cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4390d-131">Managed Disks eliminates hello limits associated with storage accounts.</span></span> <span data-ttu-id="4390d-132">Sin embargo, el número de Hola de discos administrados por suscripción es limitado too2, 000 de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="4390d-132">However, hello number of managed disks per subscription is limited too2,000 by default.</span></span> <span data-ttu-id="4390d-133">Puede llamar a tooincrease de compatibilidad con este número.</span><span class="sxs-lookup"><span data-stu-id="4390d-133">You can call support tooincrease this number.</span></span>

<span data-ttu-id="4390d-134">**¿Puedo tomar una instantánea incremental de un disco administrado?**</span><span class="sxs-lookup"><span data-stu-id="4390d-134">**Can I take an incremental snapshot of a managed disk?**</span></span>

<span data-ttu-id="4390d-135">No.</span><span class="sxs-lookup"><span data-stu-id="4390d-135">No.</span></span> <span data-ttu-id="4390d-136">capacidad de Hello corriente instantánea realiza una copia completa de un disco administrado.</span><span class="sxs-lookup"><span data-stu-id="4390d-136">hello current snapshot capability makes a full copy of a managed disk.</span></span> <span data-ttu-id="4390d-137">Sin embargo, tenemos previsto toosupport instantáneas incrementales en hello futuras.</span><span class="sxs-lookup"><span data-stu-id="4390d-137">However, we are planning toosupport incremental snapshots in hello future.</span></span>

<span data-ttu-id="4390d-138">**¿Pueden las máquinas virtuales de un conjunto de disponibilidad estar compuestas de una combinación de discos administrados y no administrados?**</span><span class="sxs-lookup"><span data-stu-id="4390d-138">**Can VMs in an availability set consist of a combination of managed and unmanaged disks?**</span></span>

<span data-ttu-id="4390d-139">No.</span><span class="sxs-lookup"><span data-stu-id="4390d-139">No.</span></span> <span data-ttu-id="4390d-140">Hola máquinas virtuales en un conjunto de disponibilidad debe usar discos todo administrados o todos los discos no administrados.</span><span class="sxs-lookup"><span data-stu-id="4390d-140">hello VMs in an availability set must use either all managed disks or all unmanaged disks.</span></span> <span data-ttu-id="4390d-141">Cuando se crea un conjunto de disponibilidad, puede elegir qué tipo de discos que desea toouse.</span><span class="sxs-lookup"><span data-stu-id="4390d-141">When you create an availability set, you can choose which type of disks you want toouse.</span></span>

<span data-ttu-id="4390d-142">**¿Está opción predeterminada de discos administrados Hola Hola portal de Azure?**</span><span class="sxs-lookup"><span data-stu-id="4390d-142">**Is Managed Disks hello default option in hello Azure portal?**</span></span>

<span data-ttu-id="4390d-143">No actualmente, pero dejará de estar predeterminado Hola Hola futuras.</span><span class="sxs-lookup"><span data-stu-id="4390d-143">Not currently, but it will become hello default in hello future.</span></span>

<span data-ttu-id="4390d-144">**¿Puedo crear un disco administrado vacío?**</span><span class="sxs-lookup"><span data-stu-id="4390d-144">**Can I create an empty managed disk?**</span></span>

<span data-ttu-id="4390d-145">Sí.</span><span class="sxs-lookup"><span data-stu-id="4390d-145">Yes.</span></span> <span data-ttu-id="4390d-146">Puede crear un disco vacío.</span><span class="sxs-lookup"><span data-stu-id="4390d-146">You can create an empty disk.</span></span> <span data-ttu-id="4390d-147">Un disco administrado puede crearse independientemente de una máquina virtual, por ejemplo, sin asociar tooa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4390d-147">A managed disk can be created independently of a VM, for example, without attaching it tooa VM.</span></span>

<span data-ttu-id="4390d-148">**¿Qué es el número de dominios de error de hello compatibles para un conjunto de disponibilidad que utiliza discos administrados?**</span><span class="sxs-lookup"><span data-stu-id="4390d-148">**What is hello supported fault domain count for an availability set that uses Managed Disks?**</span></span>

<span data-ttu-id="4390d-149">Función de la región Hola donde se encuentra conjunto de disponibilidad de Hola que utiliza discos administrados, número de dominios de error de hello admitida es 2 ó 3.</span><span class="sxs-lookup"><span data-stu-id="4390d-149">Depending on hello region where hello availability set that uses Managed Disks is located, hello supported fault domain count is 2 or 3.</span></span>

<span data-ttu-id="4390d-150">**¿Es la cuenta de almacenamiento estándar de Hola para diagnósticos configurar?**</span><span class="sxs-lookup"><span data-stu-id="4390d-150">**How is hello standard storage account for diagnostics set up?**</span></span>

<span data-ttu-id="4390d-151">Se configura una cuenta de almacenamiento privada para el diagnóstico de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="4390d-151">You set up a private storage account for VM diagnostics.</span></span> <span data-ttu-id="4390d-152">Hola futura, tenemos previsto tooswitch diagnósticos tooManaged discos también.</span><span class="sxs-lookup"><span data-stu-id="4390d-152">In hello future, we plan tooswitch diagnostics tooManaged Disks as well.</span></span>

<span data-ttu-id="4390d-153">**¿Qué tipo de compatibilidad con el Control de acceso basado en roles está disponible para Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="4390d-153">**What kind of Role-Based Access Control support is available for Managed Disks?**</span></span>

<span data-ttu-id="4390d-154">Managed Disks admite tres roles predeterminados fundamentales:</span><span class="sxs-lookup"><span data-stu-id="4390d-154">Managed Disks supports three key default roles:</span></span>

* <span data-ttu-id="4390d-155">Propietario: puede administrar todo, incluido el acceso.</span><span class="sxs-lookup"><span data-stu-id="4390d-155">Owner: Can manage everything, including access</span></span>
* <span data-ttu-id="4390d-156">Colaborador: puede administrar todo, excepto el acceso.</span><span class="sxs-lookup"><span data-stu-id="4390d-156">Contributor: Can manage everything except access</span></span>
* <span data-ttu-id="4390d-157">Lector: puede ver todo, pero no realizar cambios.</span><span class="sxs-lookup"><span data-stu-id="4390d-157">Reader: Can view everything, but can't make changes</span></span>

<span data-ttu-id="4390d-158">**¿Hay alguna manera que puedo copiar o exportar una cuenta de almacenamiento privado de disco administrado tooa?**</span><span class="sxs-lookup"><span data-stu-id="4390d-158">**Is there a way that I can copy or export a managed disk tooa private storage account?**</span></span>

<span data-ttu-id="4390d-159">Puede obtener una firma de acceso compartido de solo lectura URI para hello administrado en disco y usarlo toocopy Hola contenido tooa almacenamiento privado local o cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4390d-159">You can get a read-only shared access signature URI for hello managed disk and use it toocopy hello contents tooa private storage account or on-premises storage.</span></span>

<span data-ttu-id="4390d-160">**¿Puedo crear una copia de mi disco administrado?**</span><span class="sxs-lookup"><span data-stu-id="4390d-160">**Can I create a copy of my managed disk?**</span></span>

<span data-ttu-id="4390d-161">Los clientes pueden crear una instantánea de sus discos administrados y, a continuación, usar Hola instantánea toocreate otro disco administrado.</span><span class="sxs-lookup"><span data-stu-id="4390d-161">Customers can take a snapshot of their managed disks and then use hello snapshot toocreate another managed disk.</span></span>

<span data-ttu-id="4390d-162">**¿Siguen siendo compatibles los discos no administrados?**</span><span class="sxs-lookup"><span data-stu-id="4390d-162">**Are unmanaged disks still supported?**</span></span>

<span data-ttu-id="4390d-163">Sí.</span><span class="sxs-lookup"><span data-stu-id="4390d-163">Yes.</span></span> <span data-ttu-id="4390d-164">Admitimos discos administrados y no administrados.</span><span class="sxs-lookup"><span data-stu-id="4390d-164">We support unmanaged and managed disks.</span></span> <span data-ttu-id="4390d-165">Se recomienda que utilice discos administrados para nuevas cargas de trabajo y migrar los discos de toomanaged de las cargas de trabajo actual.</span><span class="sxs-lookup"><span data-stu-id="4390d-165">We recommend that you use managed disks for new workloads and migrate your current workloads toomanaged disks.</span></span>


<span data-ttu-id="4390d-166">**¿Si crear un disco de 128 GB y, a continuación, aumentar Hola tamaño too130 GB, se me cobrarán para el tamaño de disco siguiente hello (512 GB)?**</span><span class="sxs-lookup"><span data-stu-id="4390d-166">**If I create a 128-GB disk and then increase hello size too130 GB, will I be charged for hello next disk size (512 GB)?**</span></span>

<span data-ttu-id="4390d-167">Sí.</span><span class="sxs-lookup"><span data-stu-id="4390d-167">Yes.</span></span>

<span data-ttu-id="4390d-168">**¿Puedo crear discos administrados para el almacenamiento con redundancia local, almacenamiento con redundancia geográfica y almacenamiento con redundancia de zona?**</span><span class="sxs-lookup"><span data-stu-id="4390d-168">**Can I create locally redundant storage, geo-redundant storage, and zone-redundant storage managed disks?**</span></span>

<span data-ttu-id="4390d-169">Actualmente, Azure Managed Disks solo admite discos administrados de almacenamiento con redundancia local.</span><span class="sxs-lookup"><span data-stu-id="4390d-169">Azure Managed Disks currently supports only locally redundant storage managed disks.</span></span>

<span data-ttu-id="4390d-170">**¿Puedo reducir mis discos administrados?**</span><span class="sxs-lookup"><span data-stu-id="4390d-170">**Can I shrink or downsize my managed disks?**</span></span>

<span data-ttu-id="4390d-171">No.</span><span class="sxs-lookup"><span data-stu-id="4390d-171">No.</span></span> <span data-ttu-id="4390d-172">En la actualidad no se admite esta característica.</span><span class="sxs-lookup"><span data-stu-id="4390d-172">This feature is not supported currently.</span></span> 

<span data-ttu-id="4390d-173">**¿Puedo cambiar propiedad de nombre de equipo de hello cuando especializada (no creados mediante la herramienta de preparación del sistema de Hola o generalizado) operativo disco del sistema es tooprovision usa una máquina virtual?**</span><span class="sxs-lookup"><span data-stu-id="4390d-173">**Can I change hello computer name property when a specialized (not created by using hello System Preparation tool or generalized) operating system disk is used tooprovision a VM?**</span></span>

<span data-ttu-id="4390d-174">No.</span><span class="sxs-lookup"><span data-stu-id="4390d-174">No.</span></span> <span data-ttu-id="4390d-175">No se puede actualizar la propiedad de nombre de equipo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4390d-175">You can't update hello computer name property.</span></span> <span data-ttu-id="4390d-176">Hello nueva máquina virtual hereda, de hello primario VM, que era el disco del sistema operativo utilizado toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="4390d-176">hello new VM inherits it from hello parent VM, which was used toocreate hello operating system disk.</span></span> 

<span data-ttu-id="4390d-177">**¿Dónde puedo encontrar toocreate de plantillas de Azure Resource Manager muestra las máquinas virtuales con discos administrados?**</span><span class="sxs-lookup"><span data-stu-id="4390d-177">**Where can I find sample Azure Resource Manager templates toocreate VMs with managed disks?**</span></span>
* [<span data-ttu-id="4390d-178">Lista de plantillas mediante discos administrados</span><span class="sxs-lookup"><span data-stu-id="4390d-178">List of templates using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="4390d-179">https://github.com/chagarw/MDPP</span><span class="sxs-lookup"><span data-stu-id="4390d-179">https://github.com/chagarw/MDPP</span></span>

## <a name="managed-disks-and-storage-service-encryption"></a><span data-ttu-id="4390d-180">Managed Disks y Storage Service Encryption</span><span class="sxs-lookup"><span data-stu-id="4390d-180">Managed Disks and Storage Service Encryption</span></span> 

<span data-ttu-id="4390d-181">**¿Está habilitado el servicio Storage Service Encryption de forma predeterminada al crear un disco administrado?**</span><span class="sxs-lookup"><span data-stu-id="4390d-181">**Is Azure Storage Service Encryption enabled by default when I create a managed disk?**</span></span>

<span data-ttu-id="4390d-182">Sí.</span><span class="sxs-lookup"><span data-stu-id="4390d-182">Yes.</span></span>

<span data-ttu-id="4390d-183">**¿Que administra las claves de cifrado de hello?**</span><span class="sxs-lookup"><span data-stu-id="4390d-183">**Who manages hello encryption keys?**</span></span>

<span data-ttu-id="4390d-184">Microsoft administra las claves de cifrado de Hola.</span><span class="sxs-lookup"><span data-stu-id="4390d-184">Microsoft manages hello encryption keys.</span></span>

<span data-ttu-id="4390d-185">**¿Puedo deshabilitar Storage Service Encryption para Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="4390d-185">**Can I disable Storage Service Encryption for my managed disks?**</span></span>

<span data-ttu-id="4390d-186">No.</span><span class="sxs-lookup"><span data-stu-id="4390d-186">No.</span></span>

<span data-ttu-id="4390d-187">**¿Storage Service Encryption está solo disponible en determinadas regiones?**</span><span class="sxs-lookup"><span data-stu-id="4390d-187">**Is Storage Service Encryption only available in specific regions?**</span></span>

<span data-ttu-id="4390d-188">No.</span><span class="sxs-lookup"><span data-stu-id="4390d-188">No.</span></span> <span data-ttu-id="4390d-189">Está disponible en todas las regiones de Hola donde hay discos administrados.</span><span class="sxs-lookup"><span data-stu-id="4390d-189">It's available in all hello regions where Managed Disks is available.</span></span> <span data-ttu-id="4390d-190">Managed Disks está disponible en todas las regiones públicas y Alemania.</span><span class="sxs-lookup"><span data-stu-id="4390d-190">Managed Disks is available in all public regions and Germany.</span></span>

<span data-ttu-id="4390d-191">**¿Cómo averiguo si mi disco administrado está cifrado?**</span><span class="sxs-lookup"><span data-stu-id="4390d-191">**How can I find out if my managed disk is encrypted?**</span></span>

<span data-ttu-id="4390d-192">Puede averiguar el tiempo de hello cuando se creó un disco administrado de hello portal de Azure, hello Azure CLI y PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4390d-192">You can find out hello time when a managed disk was created from hello Azure portal, hello Azure CLI, and PowerShell.</span></span> <span data-ttu-id="4390d-193">Si es hora de hello después del 9 de junio de 2017, se cifra el disco.</span><span class="sxs-lookup"><span data-stu-id="4390d-193">If hello time is after June 9, 2017, then your disk is encrypted.</span></span> 

<span data-ttu-id="4390d-194">**¿Cómo puedo cifrar mis discos existentes que se crearon antes del 10 de junio de 2017?**</span><span class="sxs-lookup"><span data-stu-id="4390d-194">**How can I encrypt my existing disks that were created before June 10, 2017?**</span></span>

<span data-ttu-id="4390d-195">A partir del 10 de junio de 2017 escritos tooexisting administrar discos nuevos datos se cifran automáticamente.</span><span class="sxs-lookup"><span data-stu-id="4390d-195">As of June 10, 2017, new data written tooexisting managed disks is automatically encrypted.</span></span> <span data-ttu-id="4390d-196">También planeamos tooencrypt los datos existentes y cifrado de Hola se realizará de forma asincrónica en segundo plano de Hola.</span><span class="sxs-lookup"><span data-stu-id="4390d-196">We are also planning tooencrypt existing data, and hello encryption will happen asynchronously in hello background.</span></span> <span data-ttu-id="4390d-197">Si debe cifrar ahora los datos existentes, cree una copia del disco.</span><span class="sxs-lookup"><span data-stu-id="4390d-197">If you must encrypt existing data now, create a copy of your disk.</span></span> <span data-ttu-id="4390d-198">Los discos nuevos se cifrarán.</span><span class="sxs-lookup"><span data-stu-id="4390d-198">New disks will be encrypted.</span></span>

* [<span data-ttu-id="4390d-199">Copiar discos administrados mediante Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="4390d-199">Copy managed disks by using hello Azure CLI</span></span>](../articles/virtual-machines/scripts/virtual-machines-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)
* [<span data-ttu-id="4390d-200">Copia de discos administrados mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="4390d-200">Copy managed disks by using PowerShell</span></span>](../articles/virtual-machines/scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="4390d-201">**¿Están cifradas las imágenes e instantáneas administradas?**</span><span class="sxs-lookup"><span data-stu-id="4390d-201">**Are managed snapshots and images encrypted?**</span></span>

<span data-ttu-id="4390d-202">Sí.</span><span class="sxs-lookup"><span data-stu-id="4390d-202">Yes.</span></span> <span data-ttu-id="4390d-203">Todas las instantáneas e imágenes administradas creadas después del 9 de junio de 2017 se cifran automáticamente.</span><span class="sxs-lookup"><span data-stu-id="4390d-203">All managed snapshots and images created after June 9, 2017, are automatically encrypted.</span></span> 

<span data-ttu-id="4390d-204">**¿Puedo convertir máquinas virtuales con discos no administrados que se encuentran en las cuentas de almacenamiento que son o fueran discos toomanaged cifrados anteriormente?**</span><span class="sxs-lookup"><span data-stu-id="4390d-204">**Can I convert VMs with unmanaged disks that are located on storage accounts that are or were previously encrypted toomanaged disks?**</span></span>

<span data-ttu-id="4390d-205">Sí</span><span class="sxs-lookup"><span data-stu-id="4390d-205">Yes</span></span>

<span data-ttu-id="4390d-206">**¿Se cifrará también un VHD exportado de un disco administrado o de una instantánea?**</span><span class="sxs-lookup"><span data-stu-id="4390d-206">**Will an exported VHD from a managed disk or a snapshot also be encrypted?**</span></span>

<span data-ttu-id="4390d-207">No.</span><span class="sxs-lookup"><span data-stu-id="4390d-207">No.</span></span> <span data-ttu-id="4390d-208">Pero si se exporta un disco duro virtual tooan cifra cuenta de almacenamiento de un disco administrado cifrado o una instantánea, a continuación, se cifra.</span><span class="sxs-lookup"><span data-stu-id="4390d-208">But if you export a VHD tooan encrypted storage account from an encrypted managed disk or snapshot, then it's encrypted.</span></span> 

## <a name="premium-disks-managed-and-unmanaged"></a><span data-ttu-id="4390d-209">Discos premium: tanto administrados como no administrados</span><span class="sxs-lookup"><span data-stu-id="4390d-209">Premium disks: Managed and unmanaged</span></span>

<span data-ttu-id="4390d-210">**Si una máquina virtual usa una serie de tamaño que admite Premium Storage, como DSv2, ¿puedo conectar discos de datos tanto premium como estándar?**</span><span class="sxs-lookup"><span data-stu-id="4390d-210">**If a VM uses a size series that supports Premium Storage, such as a DSv2, can I attach both premium and standard data disks?**</span></span> 

<span data-ttu-id="4390d-211">Sí.</span><span class="sxs-lookup"><span data-stu-id="4390d-211">Yes.</span></span>

<span data-ttu-id="4390d-212">**¿Puedo conectar premium y series de tamaño de tooa de discos de datos estándar que no es compatible con almacenamiento Premium, por ejemplo, la serie D, Dv2, G o F?**</span><span class="sxs-lookup"><span data-stu-id="4390d-212">**Can I attach both premium and standard data disks tooa size series that doesn't support Premium Storage, such as D, Dv2, G, or F series?**</span></span>

<span data-ttu-id="4390d-213">No.</span><span class="sxs-lookup"><span data-stu-id="4390d-213">No.</span></span> <span data-ttu-id="4390d-214">Puede adjuntar solo tooVMs de discos de datos estándar que no usan una serie de tamaño que admite el almacenamiento Premium.</span><span class="sxs-lookup"><span data-stu-id="4390d-214">You can attach only standard data disks tooVMs that don't use a size series that supports Premium Storage.</span></span>

<span data-ttu-id="4390d-215">**Si creo un disco de datos premium a partir un disco duro virtual existente con 80 GB, ¿cuánto me costará?**</span><span class="sxs-lookup"><span data-stu-id="4390d-215">**If I create a premium data disk from an existing VHD that was 80 GB, how much will that cost?**</span></span>

<span data-ttu-id="4390d-216">Un disco de datos premium, creado a partir de un VHD de 80 GB se trata como el tamaño del disco premium disponibles para el siguiente hello, que es un disco P10.</span><span class="sxs-lookup"><span data-stu-id="4390d-216">A premium data disk created from an 80-GB VHD is treated as hello next-available premium disk size, which is a P10 disk.</span></span> <span data-ttu-id="4390d-217">Se le cobrará correspondiente toohello P10 disco precios.</span><span class="sxs-lookup"><span data-stu-id="4390d-217">You're charged according toohello P10 disk pricing.</span></span>

<span data-ttu-id="4390d-218">**¿Hay toouse de costos de transacción almacenamiento Premium?**</span><span class="sxs-lookup"><span data-stu-id="4390d-218">**Are there transaction costs toouse Premium Storage?**</span></span>

<span data-ttu-id="4390d-219">Existe un costo fijo para cada tamaño de disco que esté aprovisionado con límites específicos de IOPS y rendimiento.</span><span class="sxs-lookup"><span data-stu-id="4390d-219">There is a fixed cost for each disk size, which comes provisioned with specific limits on IOPS and throughput.</span></span> <span data-ttu-id="4390d-220">Hello otros costes son ancho de banda saliente y la capacidad de instantánea, si procede.</span><span class="sxs-lookup"><span data-stu-id="4390d-220">hello other costs are outbound bandwidth and snapshot capacity, if applicable.</span></span> <span data-ttu-id="4390d-221">Para obtener más información, vea hello [página de precios](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="4390d-221">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="4390d-222">**¿Cuáles son los límites de Hola para IOPS y el rendimiento que puedo recibo de caché de disco de hello?**</span><span class="sxs-lookup"><span data-stu-id="4390d-222">**What are hello limits for IOPS and throughput that I can get from hello disk cache?**</span></span>

<span data-ttu-id="4390d-223">Hola combinados límites de memoria caché y SSD local para una serie DS son 4.000 IOPS por núcleo y 33 MB por segundo por núcleo.</span><span class="sxs-lookup"><span data-stu-id="4390d-223">hello combined limits for cache and local SSD for a DS series are 4,000 IOPS per core and 33 MB per second per core.</span></span> <span data-ttu-id="4390d-224">Hola serie GS ofrece 5.000 e/s por segundo por núcleo y 50 MB por segundo por núcleo.</span><span class="sxs-lookup"><span data-stu-id="4390d-224">hello GS series offers 5,000 IOPS per core and 50 MB per second per core.</span></span>

<span data-ttu-id="4390d-225">**¿Es hello que SSD local compatibles para una máquina virtual administrado discos?**</span><span class="sxs-lookup"><span data-stu-id="4390d-225">**Is hello local SSD supported for a Managed Disks VM?**</span></span>

<span data-ttu-id="4390d-226">Hello SSD local es el almacenamiento temporal que se incluye con una máquina virtual administrada de discos.</span><span class="sxs-lookup"><span data-stu-id="4390d-226">hello local SSD is temporary storage that is included with a Managed Disks VM.</span></span> <span data-ttu-id="4390d-227">No existe ningún costo extra para este almacenamiento temporal.</span><span class="sxs-lookup"><span data-stu-id="4390d-227">There is no extra cost for this temporary storage.</span></span> <span data-ttu-id="4390d-228">Se recomienda que no utilice este toostore SSD local los datos de la aplicación porque no se conservan en almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="4390d-228">We recommend that you do not use this local SSD toostore your application data because it isn't persisted in Azure Blob storage.</span></span>

<span data-ttu-id="4390d-229">**¿Se produce las repercusiones de hello usar de RECORTE en discos premium?**</span><span class="sxs-lookup"><span data-stu-id="4390d-229">**Are there any repercussions for hello use of TRIM on premium disks?**</span></span>

<span data-ttu-id="4390d-230">No hay ningún uso de toohello inconveniente de RECORTE en discos de Azure en marcas premium o estándar.</span><span class="sxs-lookup"><span data-stu-id="4390d-230">There is no downside toohello use of TRIM on Azure disks on either premium or standard disks.</span></span>

## <a name="new-disk-sizes-managed-and-unmanaged"></a><span data-ttu-id="4390d-231">Nuevos tamaños de discos: tanto administrados como no administrados</span><span class="sxs-lookup"><span data-stu-id="4390d-231">New disk sizes: Managed and unmanaged</span></span>

<span data-ttu-id="4390d-232">**¿Cuál es el tamaño de disco más grande de Hola compatible con discos de datos y sistema operativo?**</span><span class="sxs-lookup"><span data-stu-id="4390d-232">**What is hello largest disk size supported for operating system and data disks?**</span></span>

<span data-ttu-id="4390d-233">tipo de partición de Hola que es compatible con Azure para un disco del sistema operativo es registro de arranque maestro (MBR) de Hola.</span><span class="sxs-lookup"><span data-stu-id="4390d-233">hello partition type that Azure supports for an operating system disk is hello master boot record (MBR).</span></span> <span data-ttu-id="4390d-234">formato MBR Hello es compatible con un tamaño de disco hasta too2 TB.</span><span class="sxs-lookup"><span data-stu-id="4390d-234">hello MBR format supports a disk size up too2 TB.</span></span> <span data-ttu-id="4390d-235">tamaño máximo de Hola que es compatible con Azure para un disco del sistema operativo es de 2 TB.</span><span class="sxs-lookup"><span data-stu-id="4390d-235">hello largest size that Azure supports for an operating system disk is 2 TB.</span></span> <span data-ttu-id="4390d-236">Azure admite hasta too4 TB para discos de datos.</span><span class="sxs-lookup"><span data-stu-id="4390d-236">Azure supports up too4 TB for data disks.</span></span> 

<span data-ttu-id="4390d-237">**¿Qué es Hola mayor blob tamaño de página que sea compatible?**</span><span class="sxs-lookup"><span data-stu-id="4390d-237">**What is hello largest page blob size that's supported?**</span></span>

<span data-ttu-id="4390d-238">Hola página blob tamaño máximo que admite Azure es 8 TB (8.191 GB).</span><span class="sxs-lookup"><span data-stu-id="4390d-238">hello largest page blob size that Azure supports is 8 TB (8,191 GB).</span></span> <span data-ttu-id="4390d-239">No se admiten blobs en páginas mayores de 4 TB (4.095 GB) adjuntada tooa VM como datos o discos del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="4390d-239">We don't support page blobs larger than 4 TB (4,095 GB) attached tooa VM as data or operating system disks.</span></span>

<span data-ttu-id="4390d-240">**¿Necesito toouse una nueva versión de toocreate de herramientas de Azure, conectar, cambiar el tamaño y cargar discos de más de 1 TB?**</span><span class="sxs-lookup"><span data-stu-id="4390d-240">**Do I need toouse a new version of Azure tools toocreate, attach, resize, and upload disks larger than 1 TB?**</span></span>

<span data-ttu-id="4390d-241">No es necesario tooupgrade su toocreate herramientas de Azure existente, adjuntar o cambiar el tamaño de los discos de más de 1 TB.</span><span class="sxs-lookup"><span data-stu-id="4390d-241">You don't need tooupgrade your existing Azure tools toocreate, attach, or resize disks larger than 1 TB.</span></span> <span data-ttu-id="4390d-242">tooupload de archivos desde el disco duro virtual local directamente tooAzure como un blob de página o un disco no administrado, es necesario conjuntos de herramientas más recientes de toouse hello:</span><span class="sxs-lookup"><span data-stu-id="4390d-242">tooupload your VHD file from on-premises directly tooAzure as a page blob or unmanaged disk, you need toouse hello latest tool sets:</span></span>

|<span data-ttu-id="4390d-243">Herramientas de Azure</span><span class="sxs-lookup"><span data-stu-id="4390d-243">Azure tools</span></span>      | <span data-ttu-id="4390d-244">Versiones compatibles</span><span class="sxs-lookup"><span data-stu-id="4390d-244">Supported versions</span></span>                                |
|-----------------|---------------------------------------------------|
|<span data-ttu-id="4390d-245">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4390d-245">Azure PowerShell</span></span> | <span data-ttu-id="4390d-246">Número de versión 4.1.0: versión de junio de 2017 o posterior</span><span class="sxs-lookup"><span data-stu-id="4390d-246">Version number 4.1.0: June 2017 release or later</span></span>|
|<span data-ttu-id="4390d-247">CLI de Azure v1</span><span class="sxs-lookup"><span data-stu-id="4390d-247">Azure CLI v1</span></span>     | <span data-ttu-id="4390d-248">Número de versión 0.10.13: versión de mayo de 2017 o posterior</span><span class="sxs-lookup"><span data-stu-id="4390d-248">Version number 0.10.13: May 2017 release or later</span></span>|
|<span data-ttu-id="4390d-249">AzCopy</span><span class="sxs-lookup"><span data-stu-id="4390d-249">AzCopy</span></span>           | <span data-ttu-id="4390d-250">Número de versión 6.1.0: versión de junio de 2017 o posterior</span><span class="sxs-lookup"><span data-stu-id="4390d-250">Version number 6.1.0: June 2017 release or later</span></span>|

<span data-ttu-id="4390d-251">compatibilidad con Hello v2 de CLI de Azure y Azure Storage Explorer estará disponible próximamente.</span><span class="sxs-lookup"><span data-stu-id="4390d-251">hello support for Azure CLI v2 and Azure Storage Explorer is coming soon.</span></span> 

<span data-ttu-id="4390d-252">**¿Se admiten los tamaños de disco P4 y P6 para blobs en páginas o discos no administrados?**</span><span class="sxs-lookup"><span data-stu-id="4390d-252">**Are P4 and P6 disk sizes supported for unmanaged disks or page blobs?**</span></span>

<span data-ttu-id="4390d-253">No.</span><span class="sxs-lookup"><span data-stu-id="4390d-253">No.</span></span> <span data-ttu-id="4390d-254">Los tamaños de disco P4 (32 GB) y P6 (64 GB) solo son compatibles con discos administrados.</span><span class="sxs-lookup"><span data-stu-id="4390d-254">P4 (32 GB) and P6 (64 GB) disk sizes are supported only for managed disks.</span></span> <span data-ttu-id="4390d-255">La compatibilidad para blobs en páginas y discos no administrados estará disponible próximamente.</span><span class="sxs-lookup"><span data-stu-id="4390d-255">Support for unmanaged disks and page blobs is coming soon.</span></span>

<span data-ttu-id="4390d-256">**Si mi premium existente administrado del disco de menos de 64 GB se creó antes de habilita la disco pequeño hello (alrededor de 15 de junio de 2017), ¿cómo se se factura?**</span><span class="sxs-lookup"><span data-stu-id="4390d-256">**If my existing premium managed disk less than 64 GB was created before hello small disk was enabled (around June 15, 2017), how is it billed?**</span></span>

<span data-ttu-id="4390d-257">Los discos premium pequeño existentes menor que 64 GB continuar toobe facturada correspondiente toohello P10 tarifa.</span><span class="sxs-lookup"><span data-stu-id="4390d-257">Existing small premium disks less than 64 GB continue toobe billed according toohello P10 pricing tier.</span></span> 

<span data-ttu-id="4390d-258">**¿Cómo puedo cambiar nivel de disco Hola de discos pequeños premium menor que 64 GB de tooP4 P10 o P6?**</span><span class="sxs-lookup"><span data-stu-id="4390d-258">**How can I switch hello disk tier of small premium disks less than 64 GB from P10 tooP4 or P6?**</span></span>

<span data-ttu-id="4390d-259">Puede tomar una instantánea de los discos pequeños y, a continuación, crear un Hola de conmutador de tooautomatically disco tooP4 de nivel de precios o P6 según el tamaño de hello aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="4390d-259">You can take a snapshot of your small disks and then create a disk tooautomatically switch hello pricing tier tooP4 or P6 based on hello provisioned size.</span></span> 


## <a name="what-if-my-question-isnt-answered-here"></a><span data-ttu-id="4390d-260">Mi pregunta no está respondida aquí. ¿Qué debo hacer?</span><span class="sxs-lookup"><span data-stu-id="4390d-260">What if my question isn't answered here?</span></span>

<span data-ttu-id="4390d-261">Si su pregunta no aparece aquí, háganoslo saber y lo ayudaremos a encontrar una respuesta.</span><span class="sxs-lookup"><span data-stu-id="4390d-261">If your question isn't listed here, let us know and we'll help you find an answer.</span></span> <span data-ttu-id="4390d-262">Puede publicar una pregunta final Hola de este artículo en los comentarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="4390d-262">You can post a question at hello end of this article in hello comments.</span></span> <span data-ttu-id="4390d-263">tooengage con el equipo de almacenamiento de Azure de Hola y otros miembros de la Comunidad sobre este artículo, use Hola MSDN [foro de almacenamiento de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span><span class="sxs-lookup"><span data-stu-id="4390d-263">tooengage with hello Azure Storage team and other community members about this article, use hello MSDN [Azure Storage forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span></span>

<span data-ttu-id="4390d-264">características de toorequest, enviar su solicitudes e ideas toohello [foro de comentarios de almacenamiento de Azure](https://feedback.azure.com/forums/217298-storage).</span><span class="sxs-lookup"><span data-stu-id="4390d-264">toorequest features, submit your requests and ideas toohello [Azure Storage feedback forum](https://feedback.azure.com/forums/217298-storage).</span></span>
