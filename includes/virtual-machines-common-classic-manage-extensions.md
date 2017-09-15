


## <a name="using-vm-extensions"></a><span data-ttu-id="051e5-101">Uso de extensiones de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="051e5-101">Using VM Extensions</span></span>
<span data-ttu-id="051e5-102">Las extensiones de máquina virtual de Azure implementan comportamientos o características que bien ayudan a otros programas a funcionar en máquinas virtuales de Azure (por ejemplo, la extensión **WebDeployForVSDevTest** permite Visual Studio en soluciones Web Deploy en la máquina virtual de Azure) o bien ofrecen la posibilidad de interactuar con la máquina virtual para que admita algún otro comportamiento (por ejemplo, puede usar las extensiones de acceso de máquina virtual desde PowerShell, la CLI de Azure y clientes REST para restablecer o modificar valores de acceso remoto en la máquina virtual de Azure).</span><span class="sxs-lookup"><span data-stu-id="051e5-102">Azure VM Extensions implement behaviors or features that either help other programs work on Azure VMs (for example, the **WebDeployForVSDevTest** extension allows Visual Studio to Web Deploy solutions on your Azure VM) or provide the ability for you to interact with the VM to support some other behavior (for example, you can use the VM Access extensions from PowerShell, the Azure CLI, and REST clients to reset or modify remote access values on your Azure VM).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="051e5-103">Para obtener una lista completa de las extensiones por las características que admiten, consulte [Acerca de las características y extensiones de las máquinas virtuales](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="051e5-103">For a complete list of extensions by the features they support, see [Azure VM Extensions and Features](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="051e5-104">Dado que cada extensión de máquina virtual admite una característica específica, lo que se puede y no se puede hacer exactamente con una extensión depende de la extensión.</span><span class="sxs-lookup"><span data-stu-id="051e5-104">Because each VM extension supports a specific feature, exactly what you can and cannot do with an extension depends on the extension.</span></span> <span data-ttu-id="051e5-105">Por lo tanto, antes de modificar la máquina virtual, asegúrese de leer la documentación de la extensión de máquina virtual que quiera usar.</span><span class="sxs-lookup"><span data-stu-id="051e5-105">Therefore, before modifying your VM, make sure you have read the documentation for the VM Extension you want to use.</span></span> <span data-ttu-id="051e5-106">Algunas extensiones de máquina virtual no admiten que se quiten; otras tienen propiedades que se pueden establecer y cambian radicalmente el comportamiento de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="051e5-106">Removing some VM Extensions is not supported; others have properties that can be set that change VM behavior radically.</span></span>
> 
> 

<span data-ttu-id="051e5-107">Las tareas más comunes son:</span><span class="sxs-lookup"><span data-stu-id="051e5-107">The most common tasks are:</span></span>

1. <span data-ttu-id="051e5-108">Buscar extensiones disponibles</span><span class="sxs-lookup"><span data-stu-id="051e5-108">Finding Available Extensions</span></span>
2. <span data-ttu-id="051e5-109">Actualizar extensiones cargadas</span><span class="sxs-lookup"><span data-stu-id="051e5-109">Updating Loaded Extensions</span></span>
3. <span data-ttu-id="051e5-110">Agregar extensiones</span><span class="sxs-lookup"><span data-stu-id="051e5-110">Adding Extensions</span></span>
4. <span data-ttu-id="051e5-111">Quitar extensiones</span><span class="sxs-lookup"><span data-stu-id="051e5-111">Removing Extensions</span></span>

## <a name="find-available-extensions"></a><span data-ttu-id="051e5-112">Búsqueda de extensiones disponibles</span><span class="sxs-lookup"><span data-stu-id="051e5-112">Find Available Extensions</span></span>
<span data-ttu-id="051e5-113">Puede buscar la extensión e información extendida con:</span><span class="sxs-lookup"><span data-stu-id="051e5-113">You can locate extension and extended information using:</span></span>

* <span data-ttu-id="051e5-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="051e5-114">PowerShell</span></span>
* <span data-ttu-id="051e5-115">Interfaz de la línea de comandos entre plataformas de Azure (CLI de Azure)</span><span class="sxs-lookup"><span data-stu-id="051e5-115">Azure Cross-Platform Command Line Interface (Azure CLI)</span></span>
* <span data-ttu-id="051e5-116">API de REST de administración del servicio</span><span class="sxs-lookup"><span data-stu-id="051e5-116">Service Management REST API</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="051e5-117">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="051e5-117">Azure PowerShell</span></span>
<span data-ttu-id="051e5-118">Algunas extensiones tienen cmdlets de PowerShell específicos para ellas, lo que puede facilitar su configuración en PowerShell; pero los siguientes cmdlets funcionan para todas las extensiones de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="051e5-118">Some extensions have PowerShell cmdlets that are specific to them, which may make their configuration from PowerShell easier; but the following cmdlets work for all VM extensions.</span></span>

<span data-ttu-id="051e5-119">Puede usar los cmdlets siguientes para obtener información sobre las extensiones disponibles:</span><span class="sxs-lookup"><span data-stu-id="051e5-119">You can use the following cmdlets to obtain information about available extensions:</span></span>

* <span data-ttu-id="051e5-120">Para instancias de roles web o roles de trabajo, puede usar el cmdlet [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) .</span><span class="sxs-lookup"><span data-stu-id="051e5-120">For instances of web roles or worker roles, you can use the [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet.</span></span>
* <span data-ttu-id="051e5-121">Para instancias de máquinas virtuales, puede usar el cmdlet [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) .</span><span class="sxs-lookup"><span data-stu-id="051e5-121">For instances of Virtual Machines, you can use the [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet.</span></span>
  
   <span data-ttu-id="051e5-122">En el ejemplo de código siguiente se indica cómo se muestra la información de la extensión **IaaSDiagnostics** con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="051e5-122">For example, the following code example shows how to list the information for the **IaaSDiagnostics** extension using PowerShell.</span></span>
  
      PS C:\> Get-AzureVMAvailableExtension -ExtensionName IaaSDiagnostics
  
      Publisher                   : Microsoft.Azure.Diagnostics
      ExtensionName               : IaaSDiagnostics
      Version                     : 1.2
      Label                       : Microsoft Monitoring Agent Diagnostics
      Description                 : Microsoft Monitoring Agent Extension
      PublicConfigurationSchema   :
      PrivateConfigurationSchema  :
      IsInternalExtension         : False
      SampleConfig                :
      ReplicationCompleted        : True
      Eula                        :
      PrivacyUri                  :
      HomepageUri                 :
      IsJsonExtension             : True
      DisallowMajorVersionUpgrade : False
      SupportedOS                 :
      PublishedDate               :
      CompanyName                 :

### <a name="azure-command-line-interface-azure-cli"></a><span data-ttu-id="051e5-123">Interfaz de la línea de comandos de Azure (CLI de Azure)</span><span class="sxs-lookup"><span data-stu-id="051e5-123">Azure Command Line Interface (Azure CLI)</span></span>
<span data-ttu-id="051e5-124">Algunas extensiones tienen comandos de CLI de Azure específicos para ellas (la extensión de máquina virtual de Docker es un ejemplo), lo que puede facilitar su configuración; pero los siguientes comandos funcionan para todas las extensiones de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="051e5-124">Some extensions have Azure CLI commands that are specific to them (the Docker VM Extension is one example), which may make their configuration easier; but the following commands work for all VM extensions.</span></span>

<span data-ttu-id="051e5-125">Puede usar el comando **azure vm extension list** para obtener información acerca de las extensiones disponibles y usar la opción **–-json** para mostrar toda la información disponible sobre una o varias extensiones.</span><span class="sxs-lookup"><span data-stu-id="051e5-125">You can use the **azure vm extension list** command to obtain information about available extensions, and use the **–-json** option to display all available information about one or more extensions.</span></span> <span data-ttu-id="051e5-126">Si no incluye un nombre de extensión, el comando devuelve una descripción JSON de todas las extensiones disponibles.</span><span class="sxs-lookup"><span data-stu-id="051e5-126">If you do not use an extension name, the command returns a JSON description of all available extensions.</span></span>

<span data-ttu-id="051e5-127">En el siguiente código de ejemplo se indica cómo mostrar la información de la extensión **IaaSDiagnostics** con el comando **azure vm extension list** de la CLI de Azure y cómo usar la opción **–-json** para devolver toda la información.</span><span class="sxs-lookup"><span data-stu-id="051e5-127">For example, the following code example shows how to list the information for the **IaaSDiagnostics** extension using the Azure CLI **azure vm extension list** command and uses the **–-json** option to return complete information.</span></span>

    $ azure vm extension list -n IaaSDiagnostics --json
    [
      {
        "publisher": "Microsoft.Azure.Diagnostics",
        "name": "IaaSDiagnostics",
        "version": "1.2",
        "label": "Microsoft Monitoring Agent Diagnostics",
        "description": "Microsoft Monitoring Agent Extension",
        "replicationCompleted": true,
        "isJsonExtension": true
      }
    ]



### <a name="service-management-rest-apis"></a><span data-ttu-id="051e5-128">API de REST de administración de servicios</span><span class="sxs-lookup"><span data-stu-id="051e5-128">Service Management REST APIs</span></span>
<span data-ttu-id="051e5-129">Puede usar las API de REST siguientes para obtener información sobre las extensiones disponibles:</span><span class="sxs-lookup"><span data-stu-id="051e5-129">You can use the following REST APIs to obtain information about available extensions:</span></span>

* <span data-ttu-id="051e5-130">Para instancias de roles web o roles de trabajo, puede usar la operación [Enumerar extensiones disponibles](https://msdn.microsoft.com/library/dn169559.aspx) .</span><span class="sxs-lookup"><span data-stu-id="051e5-130">For instances of web roles or worker roles, you can use the [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span> <span data-ttu-id="051e5-131">Para mostrar las versiones de las extensiones disponibles, puede usar [Enumerar versiones de extensión](https://msdn.microsoft.com/library/dn495437.aspx).</span><span class="sxs-lookup"><span data-stu-id="051e5-131">To list the versions of available extensions, you can use [List Extension Versions](https://msdn.microsoft.com/library/dn495437.aspx).</span></span>
* <span data-ttu-id="051e5-132">Para instancias de máquinas virtuales, puede usar la operación [Enumerar extensiones de recursos](https://msdn.microsoft.com/library/dn495441.aspx) .</span><span class="sxs-lookup"><span data-stu-id="051e5-132">For instances of Virtual Machines, you can use the [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span> <span data-ttu-id="051e5-133">Para mostrar las versiones de las extensiones disponibles, puede usar [Enumerar versiones de extensiones de recursos](https://msdn.microsoft.com/library/dn495440.aspx).</span><span class="sxs-lookup"><span data-stu-id="051e5-133">To list the versions of available extensions, you can use [List Resource Extension Versions](https://msdn.microsoft.com/library/dn495440.aspx).</span></span>

## <a name="add-update-or-disable-extensions"></a><span data-ttu-id="051e5-134">Adición, actualización o deshabilitación de extensiones</span><span class="sxs-lookup"><span data-stu-id="051e5-134">Add, Update, or Disable Extensions</span></span>
<span data-ttu-id="051e5-135">Las extensiones pueden agregarse cuando se crea una instancia o se pueden agregar a una instancia en ejecución.</span><span class="sxs-lookup"><span data-stu-id="051e5-135">Extensions can be added when an instance is created or they can be added to a running instance.</span></span> <span data-ttu-id="051e5-136">Las extensiones se pueden actualizar, deshabilitar o quitar.</span><span class="sxs-lookup"><span data-stu-id="051e5-136">Extensions can be updated, disabled, or removed.</span></span> <span data-ttu-id="051e5-137">Puede realizar estas acciones mediante cmdlets de Azure PowerShell o mediante operaciones de la API de REST de administración de servicios.</span><span class="sxs-lookup"><span data-stu-id="051e5-137">You can perform these actions by using Azure PowerShell cmdlets or by using the Service Management REST API operations.</span></span> <span data-ttu-id="051e5-138">Se requieren parámetros para instalar y configurar algunas extensiones.</span><span class="sxs-lookup"><span data-stu-id="051e5-138">Parameters are required to install and set up some extensions.</span></span> <span data-ttu-id="051e5-139">Se admiten parámetros públicos y privados con las extensiones.</span><span class="sxs-lookup"><span data-stu-id="051e5-139">Public and private parameters are supported for extensions.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="051e5-140">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="051e5-140">Azure PowerShell</span></span>
<span data-ttu-id="051e5-141">El uso de cmdlets de Azure PowerShell es la manera más fácil de agregar y actualizar extensiones.</span><span class="sxs-lookup"><span data-stu-id="051e5-141">Using Azure PowerShell cmdlets is the easiest way to add and update extensions.</span></span> <span data-ttu-id="051e5-142">Al usar los cmdlets de extensión, la mayor parte de la configuración de la extensión se realiza automáticamente.</span><span class="sxs-lookup"><span data-stu-id="051e5-142">When you use the extension cmdlets, most of the configuration of the extension is done for you.</span></span> <span data-ttu-id="051e5-143">En ocasiones, puede que necesite agregar una extensión mediante programación.</span><span class="sxs-lookup"><span data-stu-id="051e5-143">At times, you may need to programmatically add an extension.</span></span> <span data-ttu-id="051e5-144">En ese caso, debe proporcionar la configuración de la extensión.</span><span class="sxs-lookup"><span data-stu-id="051e5-144">When you need to do this, you must provide the configuration of the extension.</span></span>

<span data-ttu-id="051e5-145">Puede utilizar los cmdlets siguientes para saber si una extensión requiere una configuración de parámetros públicos o privados:</span><span class="sxs-lookup"><span data-stu-id="051e5-145">You can use the following cmdlets to know whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="051e5-146">Para instancias de roles web o roles de trabajo, puede usar el cmdlet **Get-AzureServiceAvailableExtension** .</span><span class="sxs-lookup"><span data-stu-id="051e5-146">For instances of web roles or worker roles, you can use the **Get-AzureServiceAvailableExtension** cmdlet.</span></span>
* <span data-ttu-id="051e5-147">Para instancias de máquinas virtuales, puede usar el cmdlet **Get-AzureVMAvailableExtension** .</span><span class="sxs-lookup"><span data-stu-id="051e5-147">For instances of Virtual Machines, you can use the **Get-AzureVMAvailableExtension** cmdlet.</span></span>

### <a name="service-management-rest-apis"></a><span data-ttu-id="051e5-148">API de REST de administración de servicios</span><span class="sxs-lookup"><span data-stu-id="051e5-148">Service Management REST APIs</span></span>
<span data-ttu-id="051e5-149">Cuando recupera una lista de extensiones disponibles mediante las API de REST, recibirá información sobre cómo se tiene que configurar la extensión.</span><span class="sxs-lookup"><span data-stu-id="051e5-149">When you retrieve a listing of available extensions by using the REST APIs, you receive information about how the extension is to be configured.</span></span> <span data-ttu-id="051e5-150">Puede que la información que se devuelva muestre información sobre parámetros representada por un esquema público y un esquema privado.</span><span class="sxs-lookup"><span data-stu-id="051e5-150">The information that is returned might show parameter information represented by a public schema and private schema.</span></span> <span data-ttu-id="051e5-151">Los valores de parámetros públicos se devuelven en las consultas sobre las instancias.</span><span class="sxs-lookup"><span data-stu-id="051e5-151">Public parameter values are returned in queries about the instances.</span></span> <span data-ttu-id="051e5-152">No se devuelven los valores de parámetros privados.</span><span class="sxs-lookup"><span data-stu-id="051e5-152">Private parameter values are not returned.</span></span>

<span data-ttu-id="051e5-153">Puede usar las API de REST siguientes para saber si una extensión requiere una configuración de parámetros públicos o privados:</span><span class="sxs-lookup"><span data-stu-id="051e5-153">You can use the following REST APIs to know whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="051e5-154">Para las instancias de roles web o roles de trabajo, los elementos **PublicConfigurationSchema** y **PrivateConfigurationSchema** contienen la información de la respuesta de la operación [Enumerar extensiones disponibles](https://msdn.microsoft.com/library/dn169559.aspx).</span><span class="sxs-lookup"><span data-stu-id="051e5-154">For instances of web roles or worker roles, the **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain the information in the response from the [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span>
* <span data-ttu-id="051e5-155">Para las instancias de Virtual Machines, los elementos **PublicConfigurationSchema** y **PrivateConfigurationSchema** contienen la información de la respuesta de la operación [Enumerar extensiones de recursos](https://msdn.microsoft.com/library/dn495441.aspx).</span><span class="sxs-lookup"><span data-stu-id="051e5-155">For instances of Virtual Machines, the **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain the information in the response from the [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span>

> [!NOTE]
> <span data-ttu-id="051e5-156">Las extensiones también pueden usar configuraciones que se definen con JSON.</span><span class="sxs-lookup"><span data-stu-id="051e5-156">Extensions can also use configurations that are defined with JSON.</span></span> <span data-ttu-id="051e5-157">Cuando se utilizan estos tipos de extensiones, solo se usa el elemento **SampleConfig** .</span><span class="sxs-lookup"><span data-stu-id="051e5-157">When these types of extensions are used, only the **SampleConfig** element is used.</span></span>
> 
> 

