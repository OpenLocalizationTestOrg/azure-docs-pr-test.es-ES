


<span data-ttu-id="c03e2-101">En este tema se describe cómo:</span><span class="sxs-lookup"><span data-stu-id="c03e2-101">This topic describes how to:</span></span>

* <span data-ttu-id="c03e2-102">Inyectar datos en una máquina virtual (VM) de Azure cuando se está aprovisionando.</span><span class="sxs-lookup"><span data-stu-id="c03e2-102">Inject data into an Azure virtual machine (VM) when it is being provisioned.</span></span>
* <span data-ttu-id="c03e2-103">Recuperarlos tanto para Windows como para Linux.</span><span class="sxs-lookup"><span data-stu-id="c03e2-103">Retrieve it for both Windows and Linux.</span></span>
* <span data-ttu-id="c03e2-104">Usar herramientas especiales disponibles en algunos sistemas toodetect y controlar automáticamente los datos personalizados.</span><span class="sxs-lookup"><span data-stu-id="c03e2-104">Use special tools available on some systems toodetect and handle custom data automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="c03e2-105">Este artículo describe cómo personalizados datos pueden insertar mediante el uso de una máquina virtual que se creó con hello API de administración de servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="c03e2-105">This article describes how custom data can be injected by using a VM created with hello Azure Service Management API.</span></span> <span data-ttu-id="c03e2-106">toosee toouse Hola API de administración de recursos de Azure, vea [plantilla de ejemplo de Hola](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span><span class="sxs-lookup"><span data-stu-id="c03e2-106">toosee how toouse hello Azure Resource Management API, see [hello example template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span></span>
> 
> 

## <a name="injecting-custom-data-into-your-azure-virtual-machine"></a><span data-ttu-id="c03e2-107">Inyección de datos personalizados en su máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="c03e2-107">Injecting custom data into your Azure virtual machine</span></span>
<span data-ttu-id="c03e2-108">Esta característica se admite actualmente solo en hello [interfaz de línea de comandos de Azure](https://github.com/Azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="c03e2-108">This feature is currently supported only in hello [Azure Command-Line Interface](https://github.com/Azure/azure-xplat-cli).</span></span> <span data-ttu-id="c03e2-109">Aquí, se crea un `custom-data.txt` archivo que contiene los datos, a continuación, insertar que en toohello VM durante el aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="c03e2-109">Here we create a `custom-data.txt` file that contains our data, then inject that in toohello VM during provisioning.</span></span> <span data-ttu-id="c03e2-110">Aunque puede utilizar cualquiera de las opciones de Hola para hello `azure vm create` comando siguiente hello muestra un enfoque muy básico:</span><span class="sxs-lookup"><span data-stu-id="c03e2-110">Although you may use any of hello options for hello `azure vm create` command, hello following demonstrates one very basic approach:</span></span>

```
    azure vm create <vmname> <vmimage> <username> <password> \  
    --location "West US" --ssh 22 \  
    --custom-data ./custom-data.txt  
```


## <a name="using-custom-data-in-hello-virtual-machine"></a><span data-ttu-id="c03e2-111">Uso de datos personalizados en la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="c03e2-111">Using custom data in hello virtual machine</span></span>
* <span data-ttu-id="c03e2-112">Si la VM de Azure es una máquina virtual basada en Windows, el archivo de datos personalizados de hello se guarda demasiado`%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span><span class="sxs-lookup"><span data-stu-id="c03e2-112">If your Azure VM is a Windows-based VM, then hello custom data file is saved too`%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span></span> <span data-ttu-id="c03e2-113">Aunque era tootransfer con codificación base64 de hello ordenador toohello nueva máquina virtual, es automáticamente descodificar y que se puede abrir o utilizar inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="c03e2-113">Although it was base64-encoded tootransfer from hello local computer toohello new VM, it is automatically decoded and can be opened or used immediately.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="c03e2-114">Si existe el archivo hello, se sobrescribe.</span><span class="sxs-lookup"><span data-stu-id="c03e2-114">If hello file exists, it is overwritten.</span></span> <span data-ttu-id="c03e2-115">seguridad de Hello en el directorio de Hola se establece demasiado**sistema: Control total** y **administradores: Control total**.</span><span class="sxs-lookup"><span data-stu-id="c03e2-115">hello security on hello directory is set too**System:Full Control** and **Administrators:Full Control**.</span></span>
  > 
  > 
* <span data-ttu-id="c03e2-116">Si la VM de Azure es una máquina virtual basadas en Linux, se encuentra el archivo de datos personalizados de hello en uno de los siguientes Hola coloca dependiendo de su distribución.</span><span class="sxs-lookup"><span data-stu-id="c03e2-116">If your Azure VM is a Linux-based VM, then hello custom data file will be located in one of hello following places depending on your distro.</span></span> <span data-ttu-id="c03e2-117">Hola pueden datos con codificación base64, por lo que puede que necesite datos de hello toodecode en primer lugar:</span><span class="sxs-lookup"><span data-stu-id="c03e2-117">hello data may be base64-encoded, so you may need toodecode hello data first:</span></span>
  
  * `/var/lib/waagent/ovf-env.xml`
  * `/var/lib/waagent/CustomData`
  * `/var/lib/cloud/instance/user-data.txt` 

## <a name="cloud-init-on-azure"></a><span data-ttu-id="c03e2-118">Cloud-init en Azure</span><span class="sxs-lookup"><span data-stu-id="c03e2-118">Cloud-init on Azure</span></span>
<span data-ttu-id="c03e2-119">Si la VM de Azure es de una imagen Ubuntu o CoreOS, a continuación, puede usar CustomData toosend una configuración de nube toocloud-init.</span><span class="sxs-lookup"><span data-stu-id="c03e2-119">If your Azure VM is from an Ubuntu or CoreOS image, then you can use CustomData toosend a cloud-config toocloud-init.</span></span> <span data-ttu-id="c03e2-120">O bien, si el archivo de datos personalizados es un script, cloud-init puede simplemente ejecutarlo.</span><span class="sxs-lookup"><span data-stu-id="c03e2-120">Or if your custom data file is a script, then cloud-init can simply execute it.</span></span>

### <a name="ubuntu-cloud-images"></a><span data-ttu-id="c03e2-121">Ubuntu Cloud Images</span><span class="sxs-lookup"><span data-stu-id="c03e2-121">Ubuntu Cloud Images</span></span>
<span data-ttu-id="c03e2-122">En la mayoría de las imágenes de Linux de Azure, debe modificar el "/ etc/waagent.conf" tooconfigure Hola temporal recurso disco y swap el archivo.</span><span class="sxs-lookup"><span data-stu-id="c03e2-122">In most Azure Linux images, you would edit "/etc/waagent.conf" tooconfigure hello temporary resource disk and swap file.</span></span> <span data-ttu-id="c03e2-123">Para más información, consulte la [Guía de usuario del Agente de Linux de Azure](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c03e2-123">See [Azure Linux Agent user guide](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information.</span></span>

<span data-ttu-id="c03e2-124">Sin embargo, en imágenes de nube de hello Ubuntu, debe usar init de la nube tooconfigure Hola recurso disco (es decir, Hola "efímero") e intercambio de partición.</span><span class="sxs-lookup"><span data-stu-id="c03e2-124">However, on hello Ubuntu Cloud Images, you must use cloud-init tooconfigure hello resource disk (that is, hello "ephemeral" disk) and swap partition.</span></span> <span data-ttu-id="c03e2-125">Vea Hola siguiente página de wiki de Ubuntu Hola para obtener más detalles: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span><span class="sxs-lookup"><span data-stu-id="c03e2-125">See hello following page on hello Ubuntu wiki for more details: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps-using-cloud-init"></a><span data-ttu-id="c03e2-126">Pasos siguientes: uso de cloud-init</span><span class="sxs-lookup"><span data-stu-id="c03e2-126">Next steps: Using cloud-init</span></span>
<span data-ttu-id="c03e2-127">Para obtener más información, vea hello [documentación init en la nube para Ubuntu](https://help.ubuntu.com/community/CloudInit).</span><span class="sxs-lookup"><span data-stu-id="c03e2-127">For further information, see hello [cloud-init documentation for Ubuntu](https://help.ubuntu.com/community/CloudInit).</span></span>

<!--Link references-->
[<span data-ttu-id="c03e2-128">Referencia de la API de REST de administración de servicios: Agregar rol</span><span class="sxs-lookup"><span data-stu-id="c03e2-128">Add Role Service Management REST API Reference</span></span>](http://msdn.microsoft.com/library/azure/jj157186.aspx)

[<span data-ttu-id="c03e2-129">Interfaz de línea de comandos de Azure</span><span class="sxs-lookup"><span data-stu-id="c03e2-129">Azure Command-line Interface</span></span>](https://github.com/Azure/azure-xplat-cli)

