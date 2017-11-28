


<span data-ttu-id="aeeea-101">En este tema se describe cómo:</span><span class="sxs-lookup"><span data-stu-id="aeeea-101">This topic describes how to:</span></span>

* <span data-ttu-id="aeeea-102">Inyectar datos en una máquina virtual (VM) de Azure cuando se está aprovisionando.</span><span class="sxs-lookup"><span data-stu-id="aeeea-102">Inject data into an Azure virtual machine (VM) when it is being provisioned.</span></span>
* <span data-ttu-id="aeeea-103">Recuperarlos tanto para Windows como para Linux.</span><span class="sxs-lookup"><span data-stu-id="aeeea-103">Retrieve it for both Windows and Linux.</span></span>
* <span data-ttu-id="aeeea-104">Usar herramientas especiales disponibles en algunos sistemas para detectar y administrar datos personalizados automáticamente.</span><span class="sxs-lookup"><span data-stu-id="aeeea-104">Use special tools available on some systems to detect and handle custom data automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="aeeea-105">En este artículo se describe cómo se pueden insertar datos personalizados mediante una máquina virtual creada con la API de Administración de servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="aeeea-105">This article describes how custom data can be injected by using a VM created with the Azure Service Management API.</span></span> <span data-ttu-id="aeeea-106">Para ver cómo se usa la API de Administración de recursos de Azure, consulte [la plantilla de ejemplo](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span><span class="sxs-lookup"><span data-stu-id="aeeea-106">To see how to use the Azure Resource Management API, see [the example template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span></span>
> 
> 

## <a name="injecting-custom-data-into-your-azure-virtual-machine"></a><span data-ttu-id="aeeea-107">Inyección de datos personalizados en su máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="aeeea-107">Injecting custom data into your Azure virtual machine</span></span>
<span data-ttu-id="aeeea-108">Esta característica solamente se admite actualmente en la [interfaz de la línea de comandos de Azure](https://github.com/Azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="aeeea-108">This feature is currently supported only in the [Azure Command-Line Interface](https://github.com/Azure/azure-xplat-cli).</span></span> <span data-ttu-id="aeeea-109">Aquí creamos un archivo `custom-data.txt` que contiene nuestros datos y después los inyectamos en la VM durante el aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="aeeea-109">Here we create a `custom-data.txt` file that contains our data, then inject that in to the VM during provisioning.</span></span> <span data-ttu-id="aeeea-110">Aunque puede usar cualquiera de las opciones para el comando `azure vm create` , a continuación se muestra un enfoque muy básico:</span><span class="sxs-lookup"><span data-stu-id="aeeea-110">Although you may use any of the options for the `azure vm create` command, the following demonstrates one very basic approach:</span></span>

```
    azure vm create <vmname> <vmimage> <username> <password> \  
    --location "West US" --ssh 22 \  
    --custom-data ./custom-data.txt  
```


## <a name="using-custom-data-in-the-virtual-machine"></a><span data-ttu-id="aeeea-111">Uso de datos personalizados en la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="aeeea-111">Using custom data in the virtual machine</span></span>
* <span data-ttu-id="aeeea-112">Si la VM de Azure es una VM Windows, el archivo de datos personalizado se guarda en `%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span><span class="sxs-lookup"><span data-stu-id="aeeea-112">If your Azure VM is a Windows-based VM, then the custom data file is saved to `%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span></span> <span data-ttu-id="aeeea-113">Aunque se codificara con base64 para transferirla del equipo local a la nueva VM, se descodifica automáticamente y se puede abrir o usar de inmediato.</span><span class="sxs-lookup"><span data-stu-id="aeeea-113">Although it was base64-encoded to transfer from the local computer to the new VM, it is automatically decoded and can be opened or used immediately.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="aeeea-114">Si el archivo existe se sobrescribe.</span><span class="sxs-lookup"><span data-stu-id="aeeea-114">If the file exists, it is overwritten.</span></span> <span data-ttu-id="aeeea-115">La seguridad del directorio se establece en **Sistema: Control total** y **Administradores: Control total**.</span><span class="sxs-lookup"><span data-stu-id="aeeea-115">The security on the directory is set to **System:Full Control** and **Administrators:Full Control**.</span></span>
  > 
  > 
* <span data-ttu-id="aeeea-116">Si la VM de Azure es una VM Linux, el archivo de datos personalizados se ubicará en uno de los dos lugares siguientes dependiendo de la distribución.</span><span class="sxs-lookup"><span data-stu-id="aeeea-116">If your Azure VM is a Linux-based VM, then the custom data file will be located in one of the following places depending on your distro.</span></span> <span data-ttu-id="aeeea-117">Los datos pueden estar codificados con base64, por lo que tiene que descifrarlos en primer lugar:</span><span class="sxs-lookup"><span data-stu-id="aeeea-117">The data may be base64-encoded, so you may need to decode the data first:</span></span>
  
  * `/var/lib/waagent/ovf-env.xml`
  * `/var/lib/waagent/CustomData`
  * `/var/lib/cloud/instance/user-data.txt` 

## <a name="cloud-init-on-azure"></a><span data-ttu-id="aeeea-118">Cloud-init en Azure</span><span class="sxs-lookup"><span data-stu-id="aeeea-118">Cloud-init on Azure</span></span>
<span data-ttu-id="aeeea-119">Si la VM de Azure procede de una imagen de Ubuntu o CoreOS, puede usar CustomData para enviar una cloud-config a cloud-init.</span><span class="sxs-lookup"><span data-stu-id="aeeea-119">If your Azure VM is from an Ubuntu or CoreOS image, then you can use CustomData to send a cloud-config to cloud-init.</span></span> <span data-ttu-id="aeeea-120">O bien, si el archivo de datos personalizados es un script, cloud-init puede simplemente ejecutarlo.</span><span class="sxs-lookup"><span data-stu-id="aeeea-120">Or if your custom data file is a script, then cloud-init can simply execute it.</span></span>

### <a name="ubuntu-cloud-images"></a><span data-ttu-id="aeeea-121">Ubuntu Cloud Images</span><span class="sxs-lookup"><span data-stu-id="aeeea-121">Ubuntu Cloud Images</span></span>
<span data-ttu-id="aeeea-122">En la mayoría de las imágenes de Linux de Azure, debe modificar "/etc/waagent.conf" para configurar el disco de recursos temporal y el archivo de intercambio.</span><span class="sxs-lookup"><span data-stu-id="aeeea-122">In most Azure Linux images, you would edit "/etc/waagent.conf" to configure the temporary resource disk and swap file.</span></span> <span data-ttu-id="aeeea-123">Para más información, consulte la [Guía de usuario del Agente de Linux de Azure](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="aeeea-123">See [Azure Linux Agent user guide](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information.</span></span>

<span data-ttu-id="aeeea-124">Sin embargo, en Ubuntu Cloud Images, debe usar cloud-init para configurar el disco de recursos (es decir, el disco "efímero") y la partición de intercambio.</span><span class="sxs-lookup"><span data-stu-id="aeeea-124">However, on the Ubuntu Cloud Images, you must use cloud-init to configure the resource disk (that is, the "ephemeral" disk) and swap partition.</span></span> <span data-ttu-id="aeeea-125">Consulte la siguiente página en la wiki de Ubuntu para obtener más detalles: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span><span class="sxs-lookup"><span data-stu-id="aeeea-125">See the following page on the Ubuntu wiki for more details: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps-using-cloud-init"></a><span data-ttu-id="aeeea-126">Pasos siguientes: uso de cloud-init</span><span class="sxs-lookup"><span data-stu-id="aeeea-126">Next steps: Using cloud-init</span></span>
<span data-ttu-id="aeeea-127">Para obtener más información, consulte la [documentación de cloud-init para Ubuntu](https://help.ubuntu.com/community/CloudInit).</span><span class="sxs-lookup"><span data-stu-id="aeeea-127">For further information, see the [cloud-init documentation for Ubuntu](https://help.ubuntu.com/community/CloudInit).</span></span>

<!--Link references-->
[<span data-ttu-id="aeeea-128">Referencia de la API de REST de administración de servicios: Agregar rol</span><span class="sxs-lookup"><span data-stu-id="aeeea-128">Add Role Service Management REST API Reference</span></span>](http://msdn.microsoft.com/library/azure/jj157186.aspx)

[<span data-ttu-id="aeeea-129">Interfaz de línea de comandos de Azure</span><span class="sxs-lookup"><span data-stu-id="aeeea-129">Azure Command-line Interface</span></span>](https://github.com/Azure/azure-xplat-cli)

