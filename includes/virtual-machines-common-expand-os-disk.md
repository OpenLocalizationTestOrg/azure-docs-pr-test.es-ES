## <a name="overview"></a><span data-ttu-id="a1268-101">Información general</span><span class="sxs-lookup"><span data-stu-id="a1268-101">Overview</span></span>
<span data-ttu-id="a1268-102">Cuando cree una nueva máquina virtual (VM) en un grupo de recursos mediante la implementación de una imagen desde [Azure Marketplace](https://azure.microsoft.com/marketplace/), la unidad del sistema operativo predeterminada es de 127 GB.</span><span class="sxs-lookup"><span data-stu-id="a1268-102">When you create a new virtual machine (VM) in a Resource Group by deploying an image from [Azure Marketplace](https://azure.microsoft.com/marketplace/), the default OS drive is 127 GB.</span></span> <span data-ttu-id="a1268-103">Aunque es posible agregar discos de datos a la máquina virtual (la cantidad depende de la SKU que haya elegido) y, además, se recomienda instalar aplicaciones y cargas de trabajo intensivas de CPU en estos discos de anexo, a menudo los clientes necesitan expandir la unidad del sistema operativo para admitir determinados escenarios, como los siguientes:</span><span class="sxs-lookup"><span data-stu-id="a1268-103">Even though it’s possible to add data disks to the VM (how many depending upon the SKU you’ve chosen) and moreover it’s recommended to install applications and CPU intensive workloads on these addendum disks, oftentimes customers need to expand the OS drive to support certain scenarios such as following:</span></span>

1. <span data-ttu-id="a1268-104">Compatibilidad con aplicaciones heredadas que instalan componentes en la unidad del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="a1268-104">Support legacy applications that install components on OS drive.</span></span>
2. <span data-ttu-id="a1268-105">Migración de una máquina virtual o un equipo físico desde local con una unidad del sistema operativo más grande.</span><span class="sxs-lookup"><span data-stu-id="a1268-105">Migrate a physical PC or virtual machine from on-premises with a larger OS drive.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a1268-106">Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: Resource Manager y el clásico.</span><span class="sxs-lookup"><span data-stu-id="a1268-106">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="a1268-107">Este artículo trata sobre el uso del modelo de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a1268-107">This article covers using the Resource Manager model.</span></span> <span data-ttu-id="a1268-108">Microsoft recomienda que las implementaciones más recientes usen el modelo del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="a1268-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> 
> 

## <a name="resize-the-os-drive"></a><span data-ttu-id="a1268-109">Cambio del tamaño de la unidad del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="a1268-109">Resize the OS drive</span></span>
<span data-ttu-id="a1268-110">En este artículo se va a realizar la tarea de cambiar el tamaño de la unidad del sistema operativo con módulos de Resource Manager de [Azure Powershell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="a1268-110">In this article we’ll accomplish the task of resizing the OS drive using resource manager modules of [Azure Powershell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="a1268-111">Abra la ventana de Powershell o Powershell ISE en el modo administrativo y siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="a1268-111">Open your Powershell ISE or Powershell window in administrative mode and follow the steps below:</span></span>

1. <span data-ttu-id="a1268-112">Inicie sesión en su cuenta de Microsoft Azure en el modo de administración de recursos y seleccione su suscripción de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="a1268-112">Sign-in to your Microsoft Azure account in resource management mode and select your subscription as follows:</span></span>
   
   ```Powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription –SubscriptionName 'my-subscription-name'
   ```
2. <span data-ttu-id="a1268-113">Configure el nombre de grupo de recursos y el nombre de la máquina virtual de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="a1268-113">Set your resource group name and VM name as follows:</span></span>
   
   ```Powershell
   $rgName = 'my-resource-group-name'
   $vmName = 'my-vm-name'
   ```
3. <span data-ttu-id="a1268-114">Obtenga una referencia a la máquina virtual de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="a1268-114">Obtain a reference to your VM as follows:</span></span>
   
   ```Powershell
   $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```
4. <span data-ttu-id="a1268-115">Detenga la máquina virtual antes de cambiar el tamaño del disco de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="a1268-115">Stop the VM before resizing the disk as follows:</span></span>
   
    ```Powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    ```
5. <span data-ttu-id="a1268-116">Este es el momento que hemos estado esperando.</span><span class="sxs-lookup"><span data-stu-id="a1268-116">And here comes the moment we’ve been waiting for!</span></span> <span data-ttu-id="a1268-117">Configure el tamaño del disco del sistema operativo en el valor deseado y actualice la máquina virtual de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="a1268-117">Set the size of the OS disk to the desired value and update the VM as follows:</span></span>
   
   ```Powershell
   $vm.StorageProfile.OSDisk.DiskSizeGB = 1023
   Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
   ```
   
   > [!WARNING]
   > <span data-ttu-id="a1268-118">El nuevo tamaño debe ser mayor que el tamaño de disco existente.</span><span class="sxs-lookup"><span data-stu-id="a1268-118">The new size should be greater than the existing disk size.</span></span> <span data-ttu-id="a1268-119">El máximo permitido es de 1023 GB.</span><span class="sxs-lookup"><span data-stu-id="a1268-119">The maximum allowed is 1023 GB.</span></span>
   > 
   > 
6. <span data-ttu-id="a1268-120">La actualización de la máquina virtual puede tardar unos segundos.</span><span class="sxs-lookup"><span data-stu-id="a1268-120">Updating the VM may take a few seconds.</span></span> <span data-ttu-id="a1268-121">Una vez que el comando acabe de ejecutarse, reinicie la máquina virtual de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="a1268-121">Once the command finishes executing, restart the VM as follows:</span></span>
   
   ```Powershell
   Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```

<span data-ttu-id="a1268-122">Eso es todo.</span><span class="sxs-lookup"><span data-stu-id="a1268-122">And that’s it!</span></span> <span data-ttu-id="a1268-123">Ahora RDP en la máquina virtual, abra Administración de equipos (o Administración de discos) y expanda la unidad utilizando el espacio recién asignado.</span><span class="sxs-lookup"><span data-stu-id="a1268-123">Now RDP into the VM, open Computer Management (or Disk Management) and expand the drive using the newly allocated space.</span></span>

## <a name="summary"></a><span data-ttu-id="a1268-124">Resumen</span><span class="sxs-lookup"><span data-stu-id="a1268-124">Summary</span></span>
<span data-ttu-id="a1268-125">En este artículo, hemos usado los módulos de Azure Resource Manager de Powershell para expandir la unidad del sistema operativo de una máquina virtual de IaaS.</span><span class="sxs-lookup"><span data-stu-id="a1268-125">In this article, we used Azure Resource Manager modules of Powershell to expand the OS drive of an IaaS virtual machine.</span></span> <span data-ttu-id="a1268-126">El script completo se muestra a continuación para su referencia:</span><span class="sxs-lookup"><span data-stu-id="a1268-126">Reproduced below is the complete script for your reference:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a1268-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a1268-127">Next Steps</span></span>
<span data-ttu-id="a1268-128">Aunque en este artículo nos centramos principalmente en expandir el disco del sistema operativo de la máquina virtual, también puede utilizarse el script desarrollado para expandir los discos de datos conectados a la máquina virtual mediante el cambio de una sola línea de código.</span><span class="sxs-lookup"><span data-stu-id="a1268-128">Though in this article, we focused primarily on expanding the OS disk of the VM, the developed script may also be used for expanding the data disks attached to the VM by changing a single line of code.</span></span> <span data-ttu-id="a1268-129">Por ejemplo, para expandir el primer disco de datos conectado a la máquina virtual, reemplace el objeto ```OSDisk``` de ```StorageProfile``` por la matriz ```DataDisks``` y utilice un índice numérico para obtener una referencia al primer disco de datos conectado, como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="a1268-129">For example, to expand the first data disk attached to the VM, replace the ```OSDisk``` object of ```StorageProfile``` with ```DataDisks``` array and use a numeric index to obtain a reference to first attached data disk, as shown below:</span></span>

```Powershell
$vm.StorageProfile.DataDisks[0].DiskSizeGB = 1023
```
<span data-ttu-id="a1268-130">Del mismo modo, puede hacer referencia a otros discos de datos conectados a la máquina virtual, ya sea mediante un índice, como se muestra arriba o con la propiedad del disco ```Name``` , como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="a1268-130">Similarly you may reference other data disks attached to the VM, either by using an index as shown above or the ```Name``` property of the disk as illustrated below:</span></span>

```Powershell
($vm.StorageProfile.DataDisks | Where {$_.Name -eq 'my-second-data-disk'})[0].DiskSizeGB = 1023
```

<span data-ttu-id="a1268-131">Si desea averiguar cómo conectar discos a una máquina virtual de Azure Resource Manager, consulte este [artículo](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a1268-131">If you want to find out how to attach disks to an Azure Resource Manager VM, check this [article](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

