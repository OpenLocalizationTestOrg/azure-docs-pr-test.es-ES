
<span data-ttu-id="6e625-101">Diagnosticar problemas relacionados con un servicio de nube de Microsoft Azure requiere la recopilación de archivos de registro del servicio de hello en máquinas virtuales cuando se producen problemas de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e625-101">Diagnosing issues with an Microsoft Azure cloud service requires collecting hello service’s log files on virtual machines as hello issues occur.</span></span> <span data-ttu-id="6e625-102">Puede usar una sola recopilación de tooperfom de hello extensión AzureLogCollector a petición de registros desde uno o más máquinas virtuales del servicio de nube (desde roles web y roles de trabajo) y transferencia Hola recopilan archivos tooan cuenta de almacenamiento de Azure, todo sin iniciar sesión en tooany de hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="6e625-102">You can use hello AzureLogCollector extension on-demand tooperfom one-time collection of logs from one or more Cloud Service VMs (from both web roles and worker roles) and transfer hello collected files tooan Azure storage account – all without remotely logging on tooany of hello VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="6e625-103">Puede encontrar descripciones para la mayoría de hello registrado información en http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.</span><span class="sxs-lookup"><span data-stu-id="6e625-103">Descriptions for most of hello logged information can be found at http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.</span></span>
> 
> 

<span data-ttu-id="6e625-104">Hay dos modos de colección depende de los tipos de Hola de toobe archivos recopilados.</span><span class="sxs-lookup"><span data-stu-id="6e625-104">There are two modes of collection dependent on hello types of files toobe collected.</span></span>

* <span data-ttu-id="6e625-105">Solo los registros del agente invitado de Azure (disponibilidad general).</span><span class="sxs-lookup"><span data-stu-id="6e625-105">Azure Guest Agent Logs only (GA).</span></span> <span data-ttu-id="6e625-106">Este modo de recopilación incluye todos los agentes de invitado tooAzure relacionados de hello registros y otros componentes de Azure.</span><span class="sxs-lookup"><span data-stu-id="6e625-106">This collection mode includes all hello logs related tooAzure guest agents and other Azure components.</span></span>
* <span data-ttu-id="6e625-107">Todos los registros (completo).</span><span class="sxs-lookup"><span data-stu-id="6e625-107">All Logs (Full).</span></span> <span data-ttu-id="6e625-108">Este modo de recopilación recopilará todos los archivos en modo GA además de:</span><span class="sxs-lookup"><span data-stu-id="6e625-108">This collection mode will collect all files in GA mode plus:</span></span>
  
  * <span data-ttu-id="6e625-109">los registros de eventos de aplicación y del sistema</span><span class="sxs-lookup"><span data-stu-id="6e625-109">system and application event logs</span></span>
  * <span data-ttu-id="6e625-110">registros de errores HTTP</span><span class="sxs-lookup"><span data-stu-id="6e625-110">HTTP error logs</span></span>
  * <span data-ttu-id="6e625-111">Registros IIS</span><span class="sxs-lookup"><span data-stu-id="6e625-111">IIS Logs</span></span>
  * <span data-ttu-id="6e625-112">Registros de configuración</span><span class="sxs-lookup"><span data-stu-id="6e625-112">Setup logs</span></span>
  * <span data-ttu-id="6e625-113">otros registros del sistema</span><span class="sxs-lookup"><span data-stu-id="6e625-113">other system logs</span></span>

<span data-ttu-id="6e625-114">En ambos modos de recopilación, se pueden especificar carpetas de la recopilación de datos adicionales mediante una colección de hello siguiendo la estructura:</span><span class="sxs-lookup"><span data-stu-id="6e625-114">In both collection modes, additional data collection folders can be specified by using a collection of hello following structure:</span></span>

* <span data-ttu-id="6e625-115">**Nombre**: Hola nombre de colección de hello, que se usará como nombre de saludo de la subcarpeta incluida toobe de archivo zip de Hola recogió.</span><span class="sxs-lookup"><span data-stu-id="6e625-115">**Name**: hello name of hello collection, which will be used as hello name of subfolder inside hello zip file toobe collected.</span></span>
* <span data-ttu-id="6e625-116">**Ubicación**: carpetas de toohello de ruta de acceso de hello en la máquina virtual de Hola donde se van a recopilar archivos.</span><span class="sxs-lookup"><span data-stu-id="6e625-116">**Location**: hello path toohello folder on hello virtual machine where file will be collected.</span></span>
* <span data-ttu-id="6e625-117">**SearchPattern**: patrón Hola de nombres de Hola de toobe archivos recopilados.</span><span class="sxs-lookup"><span data-stu-id="6e625-117">**SearchPattern**: hello pattern of hello names of files toobe collected.</span></span> <span data-ttu-id="6e625-118">El valor predeterminado es "*".</span><span class="sxs-lookup"><span data-stu-id="6e625-118">Default is “*”</span></span>
* <span data-ttu-id="6e625-119">**Recursiva**: si se van a archivos de hello recopilarán de forma recursiva en la carpeta de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e625-119">**Recursive**: if hello files will be collected recursively under hello folder.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e625-120">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6e625-120">Prerequisites</span></span>
* <span data-ttu-id="6e625-121">Necesitará toohave una cuenta de almacenamiento para archivos de extensión toosave genera zip.</span><span class="sxs-lookup"><span data-stu-id="6e625-121">You need toohave a storage account for extension toosave generated zip files.</span></span>
* <span data-ttu-id="6e625-122">Asegúrese de que está usando los cmdlets de Azure PowerShell V0.8.0 o superior.</span><span class="sxs-lookup"><span data-stu-id="6e625-122">You must make sure that you are using Azure PowerShell Cmdlets V0.8.0 or above.</span></span> <span data-ttu-id="6e625-123">Para más información, consulte [Descargas de Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="6e625-123">For more information, see [Azure Downloads](https://azure.microsoft.com/downloads/).</span></span>

## <a name="add-hello-extension"></a><span data-ttu-id="6e625-124">Agregar extensión de Hola</span><span class="sxs-lookup"><span data-stu-id="6e625-124">Add hello extension</span></span>
<span data-ttu-id="6e625-125">Puede usar [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlets o [API de REST de administración de servicios](https://msdn.microsoft.com/library/ee460799.aspx) tooadd Hola extensión AzureLogCollector.</span><span class="sxs-lookup"><span data-stu-id="6e625-125">You can use [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlets or [Service Management REST APIs](https://msdn.microsoft.com/library/ee460799.aspx) tooadd hello AzureLogCollector extension.</span></span>

<span data-ttu-id="6e625-126">Servicios de nube, Hola cmdlet de Powershell de Azure existente, **Set-AzureServiceExtension**, puede ser usado tooenable Hola extensión en instancias de rol Servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="6e625-126">For Cloud Services, hello existing Azure Powershell cmdlet, **Set-AzureServiceExtension**, can be used tooenable hello extension on Cloud Service role instances.</span></span> <span data-ttu-id="6e625-127">Cada vez que esta extensión se habilita a través de este cmdlet, recopilación de registros se desencadena en instancias de rol de hello seleccionado de los roles seleccionados.</span><span class="sxs-lookup"><span data-stu-id="6e625-127">Every time this extension is enabled through this cmdlet, log collection is triggered on hello selected role instances of selected roles.</span></span>

<span data-ttu-id="6e625-128">Para máquinas virtuales, Hola cmdlet de Powershell de Azure existente, **Set-AzureVMExtension**, puede ser la extensión de hello tooenable utilizados en máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="6e625-128">For Virtual Machines, hello existing Azure Powershell cmdlet, **Set-AzureVMExtension**, can be used tooenable hello extension on Virtual Machines.</span></span> <span data-ttu-id="6e625-129">Cada vez que esta extensión se habilita a través de los cmdlets de hello, recopilación de registros se desencadena en cada instancia.</span><span class="sxs-lookup"><span data-stu-id="6e625-129">Every time this extension is enabled through hello cmdlets, log collection is triggered on each instance.</span></span>

<span data-ttu-id="6e625-130">Internamente, esta extensión utiliza hello PublicConfiguration basada en JSON y PrivateConfiguration.</span><span class="sxs-lookup"><span data-stu-id="6e625-130">Internally, this extension uses hello JSON-based PublicConfiguration and PrivateConfiguration.</span></span> <span data-ttu-id="6e625-131">Hola aquí te mostramos diseño Hola de una muestra de JSON para la configuración pública y privada.</span><span class="sxs-lookup"><span data-stu-id="6e625-131">hello following is hello layout of a sample JSON for public and private configuration.</span></span>

### <a name="publicconfiguration"></a><span data-ttu-id="6e625-132">PublicConfiguration</span><span class="sxs-lookup"><span data-stu-id="6e625-132">PublicConfiguration</span></span>
    {
        "Instances":  "*",
        "Mode":  "Full",
        "SasUri":  "SasUri tooyour storage account with sp=wl",
        "AdditionalData":
        [
          {
                  "Name":  "StorageData",
                  "Location":  "%roleroot%storage",
                  "SearchPattern":  "*.*",
                  "Recursive":  "true"
          },
          {
                "Name":  "CustomDataFolder2",
                "Location":  "c:\customFolder",
                "SearchPattern":  "*.log",
                "Recursive":  "false"
          },
        ]
    }

### <a name="privateconfiguration"></a><span data-ttu-id="6e625-133">PrivateConfiguration</span><span class="sxs-lookup"><span data-stu-id="6e625-133">PrivateConfiguration</span></span>
    {

    }

> [!NOTE]
> <span data-ttu-id="6e625-134">Esta extensión no necesita la clase **privateConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="6e625-134">This extension doesn’t need **privateConfiguration**.</span></span> <span data-ttu-id="6e625-135">Basta con que proporcione una estructura vacía para hello **– PrivateConfiguration** argumento.</span><span class="sxs-lookup"><span data-stu-id="6e625-135">You can just provide an empty structure for hello **–PrivateConfiguration** argument.</span></span>
> 
> 

<span data-ttu-id="6e625-136">Puede seguir uno de dos Hola siguiendo los pasos tooadd hello AzureLogCollector tooone o más instancias de un servicio de nube o una máquina Virtual de los roles seleccionados, los desencadenadores que Hola recopilaciones en cada máquina virtual toorun y envían archivos de hello recopilan tooAzure cuenta especificado.</span><span class="sxs-lookup"><span data-stu-id="6e625-136">You can follow one of hello two following steps tooadd hello AzureLogCollector tooone or more instances of a Cloud Service or Virtual Machine of selected roles, which triggers hello collections on each VM toorun and send hello collected files tooAzure account specified.</span></span>

## <a name="adding-as-a-service-extension"></a><span data-ttu-id="6e625-137">Agregar como extensión de servicio</span><span class="sxs-lookup"><span data-stu-id="6e625-137">Adding as a Service Extension</span></span>
1. <span data-ttu-id="6e625-138">Siga suscripción tooyour de hello instrucciones tooconnect PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="6e625-138">Follow hello instructions tooconnect Azure PowerShell tooyour subscription.</span></span>
2. <span data-ttu-id="6e625-139">Especifique el nombre del servicio de hello, ranura, roles y toowhich de instancias de rol que desee tooadd y habilitar la extensión de hello AzureLogCollector.</span><span class="sxs-lookup"><span data-stu-id="6e625-139">Specify hello service name, slot, roles, and role instances toowhich you want tooadd and enable hello AzureLogCollector extension.</span></span>
   
        #Specify your cloud service name
        $ServiceName = 'extensiontest2'
   
        #Specify hello slot. 'Production' or 'Staging'
        $slot = 'Production'
   
        #Specified hello roles on which hello extension will be installed and enabled
        $roles = @("WorkerRole1","WebRole1")
   
        #Specify hello instances on which extension will be installed and enabled.  Use wildcard * for all instances
        $instances = @("*")
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
3. <span data-ttu-id="6e625-140">Especificar la carpeta de datos adicionales de hello para el que se van a recopilar archivos (este paso es opcional).</span><span class="sxs-lookup"><span data-stu-id="6e625-140">Specify hello additional data folder for which files will be collected (this step is optional).</span></span>
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
   
   > [!NOTE]
   > <span data-ttu-id="6e625-141">Puede usar el token `%roleroot%` toospecify Hola unidad raíz del rol ya que no utiliza una unidad fija.</span><span class="sxs-lookup"><span data-stu-id="6e625-141">You can use token `%roleroot%` toospecify hello role root drive since it doesn’t use a fixed drive.</span></span>
   > 
   > 
4. <span data-ttu-id="6e625-142">Proporcione el nombre de cuenta de almacenamiento de Azure de Hola y archivos de clave toowhich recopilado se cargará.</span><span class="sxs-lookup"><span data-stu-id="6e625-142">Provide hello Azure storage account name and key toowhich collected files will be uploaded.</span></span>
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
5. <span data-ttu-id="6e625-143">Llame a hello SetAzureServiceLogCollector.ps1 (incluido al final de hello del artículo hello) como extensión de sigue tooenable hello AzureLogCollector para un servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="6e625-143">Call hello SetAzureServiceLogCollector.ps1 (included at hello end of hello article) as follows tooenable hello AzureLogCollector extension for a Cloud Service.</span></span> <span data-ttu-id="6e625-144">Una vez que haya completado la ejecución de hello, puede encontrar Hola cargar archivos en`https://YouareStorageAccountName.blob.core.windows.net/vmlogs`</span><span class="sxs-lookup"><span data-stu-id="6e625-144">Once hello execution is completed, you can find hello uploaded file under `https://YouareStorageAccountName.blob.core.windows.net/vmlogs`</span></span>
   
        .\SetAzureServiceLogCollector.ps1 -ServiceName YourCloudServiceName  -Roles $roles  -Instances $instances –Mode $mode -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey -AdditionDataLocationList $AdditionalDataList

<span data-ttu-id="6e625-145">Hola aquí te mostramos definición Hola de parámetros de hello pasados toohello script.</span><span class="sxs-lookup"><span data-stu-id="6e625-145">hello following is hello definition of hello parameters passed toohello script.</span></span> <span data-ttu-id="6e625-146">(También se copia a continuación).</span><span class="sxs-lookup"><span data-stu-id="6e625-146">(This is copied below as well.)</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
      [Parameter(Mandatory=$true)]
    [string]   $ServiceName,

    [Parameter(Mandatory=$false)]
    [string[]] $Roles ,

    [Parameter(Mandatory=$false)]
    [string[]] $Instances,

    [Parameter(Mandatory=$false)]
    [string]   $Slot = 'Production',

    [Parameter(Mandatory=$false)]
    [string]   $Mode = 'Full',

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountName,

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountKey,

    [Parameter(Mandatory=$false)]
    [PSObject[]] $AdditionDataLocationList = $null
    )

* <span data-ttu-id="6e625-147">*ServiceName*: el nombre del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="6e625-147">*ServiceName*: Your cloud service name.</span></span>
* <span data-ttu-id="6e625-148">*Roles*: una lista de roles, como "WebRole1" o "WorkerRole1".</span><span class="sxs-lookup"><span data-stu-id="6e625-148">*Roles*: A list of roles, such as “WebRole1” or ”WorkerRole1”.</span></span>
* <span data-ttu-id="6e625-149">*Instancias*: una lista de nombres de Hola de instancias de rol separados por coma: utilice la cadena de caracteres comodín de hello ("*") para todas las instancias de rol.</span><span class="sxs-lookup"><span data-stu-id="6e625-149">*Instances*: A list of hello names of role instances separated by comma -- use hello wildcard string (“*”) for all role instances.</span></span>
* <span data-ttu-id="6e625-150">*Slot*: nombre de la ranura.</span><span class="sxs-lookup"><span data-stu-id="6e625-150">*Slot*: Slot name.</span></span> <span data-ttu-id="6e625-151">“Production” o “Staging”.</span><span class="sxs-lookup"><span data-stu-id="6e625-151">“Production” or “Staging”.</span></span>
* <span data-ttu-id="6e625-152">*Mode*: modo de recopilación.</span><span class="sxs-lookup"><span data-stu-id="6e625-152">*Mode*: Collection mode.</span></span> <span data-ttu-id="6e625-153">“Full” o “GA”.</span><span class="sxs-lookup"><span data-stu-id="6e625-153">“Full” or “GA”.</span></span>
* <span data-ttu-id="6e625-154">*StorageAccountName*: nombre de la cuenta de almacenamiento de Azure para almacenar los datos recopilados.</span><span class="sxs-lookup"><span data-stu-id="6e625-154">*StorageAccountName*: Name of Azure storage account for storing collected data.</span></span>
* <span data-ttu-id="6e625-155">*StorageAccountKey*: nombre de la clave de la cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="6e625-155">*StorageAccountKey*: Name of Azure storage account key.</span></span>
* <span data-ttu-id="6e625-156">*AdditionalDataLocationList*: una lista de hello siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="6e625-156">*AdditionalDataLocationList*: A list of hello following structure:</span></span>
  
      {
      String Name,
      String Location,
      String SearchPattern,
      Bool   Recursive
      }

## <a name="adding-as-a-vm-extension"></a><span data-ttu-id="6e625-157">Agregar como extensión de servicio de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="6e625-157">Adding as a VM Extension</span></span>
<span data-ttu-id="6e625-158">Siga suscripción tooyour de hello instrucciones tooconnect PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="6e625-158">Follow hello instructions tooconnect Azure PowerShell tooyour subscription.</span></span>

1. <span data-ttu-id="6e625-159">Especifique el nombre del servicio de hello, la VM y modo de recopilación de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e625-159">Specify hello service name, VM, and hello collection mode.</span></span>
   
        #Specify your cloud service name
        $ServiceName = 'YourCloudServiceName'
   
        #Specify hello VM name
        $VMName = "'YourVMName'"
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
   
        Specify hello additional data folder for which files will be collected (this step is optional).
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
2. <span data-ttu-id="6e625-160">Proporcione el nombre de cuenta de almacenamiento de Azure de Hola y archivos de clave toowhich recopilado se cargará.</span><span class="sxs-lookup"><span data-stu-id="6e625-160">Provide hello Azure storage account name and key toowhich collected files will be uploaded.</span></span>
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
3. <span data-ttu-id="6e625-161">Llame a hello SetAzureVMLogCollector.ps1 (incluido al final de hello del artículo hello) como extensión de sigue tooenable hello AzureLogCollector para un servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="6e625-161">Call hello SetAzureVMLogCollector.ps1 (included at hello end of hello article) as follows tooenable hello AzureLogCollector extension for a Cloud Service.</span></span> <span data-ttu-id="6e625-162">Una vez que haya completado la ejecución de hello, puede encontrar el archivo de hello cargado en https://YouareStorageAccountName.BLOB.Core.Windows.NET/vmlogs</span><span class="sxs-lookup"><span data-stu-id="6e625-162">Once hello execution is completed, you can find hello uploaded file under https://YouareStorageAccountName.blob.core.windows.net/vmlogs</span></span>

<span data-ttu-id="6e625-163">Hola aquí te mostramos definición Hola de parámetros de hello pasados toohello script.</span><span class="sxs-lookup"><span data-stu-id="6e625-163">hello following is hello definition of hello parameters passed toohello script.</span></span> <span data-ttu-id="6e625-164">(También se copia a continuación).</span><span class="sxs-lookup"><span data-stu-id="6e625-164">(This is copied below as well.)</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
        [Parameter(Mandatory=$true)]
      [string]   $ServiceName,

      [Parameter(Mandatory=$false)]
      [string] $VMName ,

        [Parameter(Mandatory=$false)]
      [string]   $Mode = 'Full',

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountName,

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountKey,

      [Parameter(Mandatory=$false)]
      [PSObject[]] $AdditionDataLocationList = $null
      )

* <span data-ttu-id="6e625-165">ServiceName: nombre del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="6e625-165">ServiceName: Your cloud service name.</span></span>
* <span data-ttu-id="6e625-166">Nombre de hello VMName de hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6e625-166">VMName hello name of hello VM.</span></span>
* <span data-ttu-id="6e625-167">Mode: modo de recopilación.</span><span class="sxs-lookup"><span data-stu-id="6e625-167">Mode: Collection mode.</span></span> <span data-ttu-id="6e625-168">“Full” o “GA”.</span><span class="sxs-lookup"><span data-stu-id="6e625-168">“Full” or “GA”.</span></span>
* <span data-ttu-id="6e625-169">StorageAccountName: nombre de la cuenta de almacenamiento de Azure para almacenar los datos recopilados.</span><span class="sxs-lookup"><span data-stu-id="6e625-169">StorageAccountName: Name of Azure storage account for storing collected data.</span></span>
* <span data-ttu-id="6e625-170">StorageAccountKey: nombre de la clave de la cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="6e625-170">StorageAccountKey: Name of Azure storage account key.</span></span>
* <span data-ttu-id="6e625-171">AdditionalDataLocationList: Una lista de hello siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="6e625-171">AdditionalDataLocationList: A list of hello following structure:</span></span>

```
      {
        String Name,
        String Location,
        String SearchPattern,
        Bool   Recursive
      }
```

## <a name="extention-powershell-script-files"></a><span data-ttu-id="6e625-172">Archivos del script de PowerShell de extensión</span><span class="sxs-lookup"><span data-stu-id="6e625-172">Extention PowerShell Script files</span></span>
<span data-ttu-id="6e625-173">SetAzureServiceLogCollector.ps1</span><span class="sxs-lookup"><span data-stu-id="6e625-173">SetAzureServiceLogCollector.ps1</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Roles ,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Instances = '*',

                  [Parameter(Mandatory=$false)]
                  [string]   $Slot = 'Production',

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject

    if ($Instances -ne $null -and $Instances.Count -gt 0)  #Instances should be seperated by ,
    {
        $instanceText = $Instances[0]
        for ($i = 1;$i -lt $Instances.Count;$i++)
        {
              $instanceText = $instanceText+ "," + $Instances[$i]
          }
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value $instanceText
    }
    else  #For all instances if not specified.  hello value should be a space or *
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value " "
    }

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need tooget hello Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json
    "publicConfig is:  $publicConfigJSON"

    #we just provide a empty privateConfig object
    $privateconfig = "{
    }"

    if ($Roles -ne $null)
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot -Role $Roles -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }
    else
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot  -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }

    #
    #This is an optional step: generate a sasUri toohello container so it can be shared with other people if nened
    #
    $SasExpireTime = [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rl -Context $context
    $SasUri = $SasUri + "&restype=container&comp=list"
    Write-Output "hello container for uploaded file can be accessed using this link:`r`n$sasuri"


<span data-ttu-id="6e625-174">SetAzureVMLogCollector.ps1</span><span class="sxs-lookup"><span data-stu-id="6e625-174">SetAzureVMLogCollector.ps1</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string] $VMName ,

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject
    $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value "*"

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need tooget hello Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(90).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json

    Write-Output "PublicConfigurtion is: \r\n$publicConfigJSON"

    #
    #we just provide a empty privateConfig object
    #
    $privateconfig = "{
    }"

    if ($VMName -ne $null )
    {
          $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
          $VM.VM.OSVirtualHardDisk.OS

          if ($VM.VM.OSVirtualHardDisk.OS -like '*Windows*')
          {
                Set-AzureVMExtension -VM $VM -ExtensionName "AzureLogCollector" -Publisher Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.* | Update-AzureVM -Verbose

                #
                #We will check hello VM status toofind if operation by extension has been completed or not. hello completion of hello operation,either succeed or fail, can be indicated by
                #hello presence of SubstatusList field.
                #
                $Completed = $false
                while ($Completed -ne $true)
                {
                        $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
                        $status = $VM.ResourceExtensionStatusList | Where-Object {$_.HandlerName -eq "Microsoft.WindowsAzure.Compute.AzureLogCollector"}

                        if ( ($status.Code -ne 0) -and ($status.Status -like '*error*'))
                        {
                            Write-Output "Error status is returned: $($Status.ExtensionSettingStatus.FormattedMessage.Message)."
                              $Completed = $true
                        }
                        elseif (($status.ExtensionSettingStatus.SubstatusList -eq $null -or $status.ExtensionSettingStatus.SubstatusList.Count -lt 1))
                        {
                              $Completed = $false
                              Write-Output "Waiting for operation toocomplete..."
                        }
                        else
                        {
                              $Completed = $true
                              Write-Output "Operation completed."

                        $UploadedFileUri = $Status.ExtensionSettingStatus.SubStatusList[0].FormattedMessage.Message
                              $blob = New-Object Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob($UploadedFileUri)

                      #
                            # This is an optional step:  For easier access toohello file, we can generate a read-only SasUri directly toohello file
                              #
                              $ExpiryTimeRead =  [DateTime]::Now.AddMinutes(120).ToString("o")
                              $ReadSasUri = New-AzureStorageBlobSASToken -ExpiryTime $ExpiryTimeRead  -FullUri  -Blob  $blob.name -Container $blob.Container.Name -Permission r -Context $context

                            Write-Output "hello uploaded file can be accessed using this link: $ReadSasUri"

                              #
                              #This is an optional step:  Remove hello extension after we are done
                              #
                              Get-AzureVM -ServiceName $ServiceName -Name $VMName | Set-AzureVMExtension -Publisher Microsoft.WindowsAzure.Compute -ExtensionName "AzureLogCollector" -Version 1.* -Uninstall | Update-AzureVM -Verbose

                        }
                        Start-Sleep -s 5
                }
          }
          else
          {
              Write-Output "VM OS Type is not Windows, hello extension cannot be enabled"
          }

    }
    else
    {
      Write-Output "VM name is not specified, hello extension cannot be enabled"
    }

## <a name="next-steps"></a><span data-ttu-id="6e625-175">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6e625-175">Next Steps</span></span>
<span data-ttu-id="6e625-176">Ahora puede examinar o copiar los registros desde una ubicación muy sencilla.</span><span class="sxs-lookup"><span data-stu-id="6e625-176">Now you can examine or copy your logs from one very simple location.</span></span>

