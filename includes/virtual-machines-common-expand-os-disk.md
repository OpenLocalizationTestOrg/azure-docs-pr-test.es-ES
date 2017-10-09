## <a name="overview"></a><span data-ttu-id="76a6a-101">Información general</span><span class="sxs-lookup"><span data-stu-id="76a6a-101">Overview</span></span>
<span data-ttu-id="76a6a-102">Cuando se crea una nueva máquina virtual (VM) en un grupo de recursos mediante la implementación de una imagen de [Azure Marketplace](https://azure.microsoft.com/marketplace/), unidad de sistema operativo de hello predeterminada es 127 GB.</span><span class="sxs-lookup"><span data-stu-id="76a6a-102">When you create a new virtual machine (VM) in a Resource Group by deploying an image from [Azure Marketplace](https://azure.microsoft.com/marketplace/), hello default OS drive is 127 GB.</span></span> <span data-ttu-id="76a6a-103">Aunque es posible tooadd datos discos toohello VM (según cuántos Hola SKU que ha elegido) y además es tooinstall recomendada aplicaciones y cargas de trabajo intensivas de CPU en estos discos anexo, a menudo los clientes necesitan tooexpand Hola SO unidad toosupport determinados escenarios como la siguiente:</span><span class="sxs-lookup"><span data-stu-id="76a6a-103">Even though it’s possible tooadd data disks toohello VM (how many depending upon hello SKU you’ve chosen) and moreover it’s recommended tooinstall applications and CPU intensive workloads on these addendum disks, oftentimes customers need tooexpand hello OS drive toosupport certain scenarios such as following:</span></span>

1. <span data-ttu-id="76a6a-104">Compatibilidad con aplicaciones heredadas que instalan componentes en la unidad del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="76a6a-104">Support legacy applications that install components on OS drive.</span></span>
2. <span data-ttu-id="76a6a-105">Migración de una máquina virtual o un equipo físico desde local con una unidad del sistema operativo más grande.</span><span class="sxs-lookup"><span data-stu-id="76a6a-105">Migrate a physical PC or virtual machine from on-premises with a larger OS drive.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="76a6a-106">Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: Resource Manager y el clásico.</span><span class="sxs-lookup"><span data-stu-id="76a6a-106">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="76a6a-107">Este artículo incluye el uso de modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="76a6a-107">This article covers using hello Resource Manager model.</span></span> <span data-ttu-id="76a6a-108">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="76a6a-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> 
> 

## <a name="resize-hello-os-drive"></a><span data-ttu-id="76a6a-109">Cambiar el tamaño de unidad de hello SO</span><span class="sxs-lookup"><span data-stu-id="76a6a-109">Resize hello OS drive</span></span>
<span data-ttu-id="76a6a-110">En este artículo se podrá llevar a cabo la tarea hello de cambiar el tamaño de unidad de hello SO mediante módulos de administrador de recursos de [Azure Powershell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="76a6a-110">In this article we’ll accomplish hello task of resizing hello OS drive using resource manager modules of [Azure Powershell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="76a6a-111">Abra el ISE de Powershell o la ventana de Powershell en modo de administrador y siga Hola pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="76a6a-111">Open your Powershell ISE or Powershell window in administrative mode and follow hello steps below:</span></span>

1. <span data-ttu-id="76a6a-112">Inicio de sesión tooyour Microsoft Azure en modo de administración de recursos de la cuenta y seleccione su suscripción como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="76a6a-112">Sign-in tooyour Microsoft Azure account in resource management mode and select your subscription as follows:</span></span>
   
   ```Powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription –SubscriptionName 'my-subscription-name'
   ```
2. <span data-ttu-id="76a6a-113">Configure el nombre de grupo de recursos y el nombre de la máquina virtual de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="76a6a-113">Set your resource group name and VM name as follows:</span></span>
   
   ```Powershell
   $rgName = 'my-resource-group-name'
   $vmName = 'my-vm-name'
   ```
3. <span data-ttu-id="76a6a-114">Obtener un tooyour referencia VM como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="76a6a-114">Obtain a reference tooyour VM as follows:</span></span>
   
   ```Powershell
   $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```
4. <span data-ttu-id="76a6a-115">Detener Hola VM antes de cambiar el tamaño de disco de hello como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="76a6a-115">Stop hello VM before resizing hello disk as follows:</span></span>
   
    ```Powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    ```
5. <span data-ttu-id="76a6a-116">Y aquí viene momento Hola que nos hemos estado esperando.</span><span class="sxs-lookup"><span data-stu-id="76a6a-116">And here comes hello moment we’ve been waiting for!</span></span> <span data-ttu-id="76a6a-117">Establecer tamaño de Hola de valor de hello SO discos toohello deseado y actualizar Hola VM como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="76a6a-117">Set hello size of hello OS disk toohello desired value and update hello VM as follows:</span></span>
   
   ```Powershell
   $vm.StorageProfile.OSDisk.DiskSizeGB = 1023
   Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
   ```
   
   > [!WARNING]
   > <span data-ttu-id="76a6a-118">Hola nuevo tamaño debe ser mayor que el tamaño del disco de hello existente.</span><span class="sxs-lookup"><span data-stu-id="76a6a-118">hello new size should be greater than hello existing disk size.</span></span> <span data-ttu-id="76a6a-119">Hola máximo permitido es de 1023 GB.</span><span class="sxs-lookup"><span data-stu-id="76a6a-119">hello maximum allowed is 1023 GB.</span></span>
   > 
   > 
6. <span data-ttu-id="76a6a-120">Hola actualizando máquina virtual puede tardar unos segundos.</span><span class="sxs-lookup"><span data-stu-id="76a6a-120">Updating hello VM may take a few seconds.</span></span> <span data-ttu-id="76a6a-121">Una vez que el comando hello termina de ejecutarse, reinicie Hola VM como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="76a6a-121">Once hello command finishes executing, restart hello VM as follows:</span></span>
   
   ```Powershell
   Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```

<span data-ttu-id="76a6a-122">Eso es todo.</span><span class="sxs-lookup"><span data-stu-id="76a6a-122">And that’s it!</span></span> <span data-ttu-id="76a6a-123">Ahora RDP en Hola de máquina virtual, abra Administración de equipos (o administración de discos) y expanda la unidad de hello mediante Hola espacio recién asignado.</span><span class="sxs-lookup"><span data-stu-id="76a6a-123">Now RDP into hello VM, open Computer Management (or Disk Management) and expand hello drive using hello newly allocated space.</span></span>

## <a name="summary"></a><span data-ttu-id="76a6a-124">Resumen</span><span class="sxs-lookup"><span data-stu-id="76a6a-124">Summary</span></span>
<span data-ttu-id="76a6a-125">En este artículo, se usan Azure Resource Manager módulos de Powershell tooexpand hello unidad de sistema operativo de una máquina virtual de IaaS.</span><span class="sxs-lookup"><span data-stu-id="76a6a-125">In this article, we used Azure Resource Manager modules of Powershell tooexpand hello OS drive of an IaaS virtual machine.</span></span> <span data-ttu-id="76a6a-126">Reproducir a continuación es el script completo de Hola para su referencia:</span><span class="sxs-lookup"><span data-stu-id="76a6a-126">Reproduced below is hello complete script for your reference:</span></span>

```Powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName 'my-subscription-name'
$rgName = 'my-resource-group-name'
$vmName = 'my-vm-name'
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
$vm.StorageProfile.OSDisk.DiskSizeGB = 1023
Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```

## <a name="next-steps"></a><span data-ttu-id="76a6a-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="76a6a-127">Next Steps</span></span>
<span data-ttu-id="76a6a-128">Aunque en este artículo, nos centramos principalmente en disco Hola SO de hello VM de expansión, hello desarrollado script también se puede usar para cambiar una sola línea de código de expansión Hola datos discos conectados toohello VM.</span><span class="sxs-lookup"><span data-stu-id="76a6a-128">Though in this article, we focused primarily on expanding hello OS disk of hello VM, hello developed script may also be used for expanding hello data disks attached toohello VM by changing a single line of code.</span></span> <span data-ttu-id="76a6a-129">Por ejemplo, tooexpand Hola primero los datos toohello adjunto VM de disco, reemplace hello ```OSDisk``` objeto de ```StorageProfile``` con ```DataDisks``` de matriz y usar un tooobtain índice numérico un disco de datos adjuntos de toofirst de referencia, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="76a6a-129">For example, tooexpand hello first data disk attached toohello VM, replace hello ```OSDisk``` object of ```StorageProfile``` with ```DataDisks``` array and use a numeric index tooobtain a reference toofirst attached data disk, as shown below:</span></span>

```Powershell
$vm.StorageProfile.DataDisks[0].DiskSizeGB = 1023
```
<span data-ttu-id="76a6a-130">Del mismo modo puede hacer referencia a otro discos de datos adjunto toohello virtual, ya sea mediante un índice, como se muestra arriba u Hola ```Name``` propiedad del disco de hello tal como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="76a6a-130">Similarly you may reference other data disks attached toohello VM, either by using an index as shown above or hello ```Name``` property of hello disk as illustrated below:</span></span>

```Powershell
($vm.StorageProfile.DataDisks | Where {$_.Name -eq 'my-second-data-disk'})[0].DiskSizeGB = 1023
```

<span data-ttu-id="76a6a-131">Active esta casilla si desea toofind out cómo tooattach discos tooan VM de Azure Resource Manager, [artículo](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="76a6a-131">If you want toofind out how tooattach disks tooan Azure Resource Manager VM, check this [article](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

