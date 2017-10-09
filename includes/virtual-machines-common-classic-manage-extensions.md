


## <a name="using-vm-extensions"></a><span data-ttu-id="bfa24-101">Uso de extensiones de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="bfa24-101">Using VM Extensions</span></span>
<span data-ttu-id="bfa24-102">Extensiones de VM de Azure implementan comportamientos o características que ya sea ayudan a otros programas a trabajar en máquinas virtuales de Azure (por ejemplo, hello **WebDeployForVSDevTest** extensión permite implementar soluciones tooWeb de Visual Studio en la VM de Azure) o proporcionar Hola capacidad para toointeract con hello VM toosupport algún otro comportamiento (por ejemplo, puede usar las extensiones de acceso de VM de Hola de PowerShell, hello Azure CLI y tooreset de los clientes REST o modificar valores de acceso remoto en la VM de Azure).</span><span class="sxs-lookup"><span data-stu-id="bfa24-102">Azure VM Extensions implement behaviors or features that either help other programs work on Azure VMs (for example, hello **WebDeployForVSDevTest** extension allows Visual Studio tooWeb Deploy solutions on your Azure VM) or provide hello ability for you toointeract with hello VM toosupport some other behavior (for example, you can use hello VM Access extensions from PowerShell, hello Azure CLI, and REST clients tooreset or modify remote access values on your Azure VM).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bfa24-103">Para obtener una lista completa de las extensiones de características de Hola que admiten, consulte [características y extensiones de VM de Azure](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bfa24-103">For a complete list of extensions by hello features they support, see [Azure VM Extensions and Features](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="bfa24-104">Dado que cada extensión de VM admite una característica específica, exactamente lo que puede y no puede realizar con una extensión depende Hola extensión.</span><span class="sxs-lookup"><span data-stu-id="bfa24-104">Because each VM extension supports a specific feature, exactly what you can and cannot do with an extension depends on hello extension.</span></span> <span data-ttu-id="bfa24-105">Por lo tanto, antes de modificar la máquina virtual, asegúrese de que ha leído documentación Hola Hola extensión de máquina virtual que desee toouse.</span><span class="sxs-lookup"><span data-stu-id="bfa24-105">Therefore, before modifying your VM, make sure you have read hello documentation for hello VM Extension you want toouse.</span></span> <span data-ttu-id="bfa24-106">Algunas extensiones de máquina virtual no admiten que se quiten; otras tienen propiedades que se pueden establecer y cambian radicalmente el comportamiento de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bfa24-106">Removing some VM Extensions is not supported; others have properties that can be set that change VM behavior radically.</span></span>
> 
> 

<span data-ttu-id="bfa24-107">Hola las tareas más comunes son:</span><span class="sxs-lookup"><span data-stu-id="bfa24-107">hello most common tasks are:</span></span>

1. <span data-ttu-id="bfa24-108">Buscar extensiones disponibles</span><span class="sxs-lookup"><span data-stu-id="bfa24-108">Finding Available Extensions</span></span>
2. <span data-ttu-id="bfa24-109">Actualizar extensiones cargadas</span><span class="sxs-lookup"><span data-stu-id="bfa24-109">Updating Loaded Extensions</span></span>
3. <span data-ttu-id="bfa24-110">Agregar extensiones</span><span class="sxs-lookup"><span data-stu-id="bfa24-110">Adding Extensions</span></span>
4. <span data-ttu-id="bfa24-111">Quitar extensiones</span><span class="sxs-lookup"><span data-stu-id="bfa24-111">Removing Extensions</span></span>

## <a name="find-available-extensions"></a><span data-ttu-id="bfa24-112">Búsqueda de extensiones disponibles</span><span class="sxs-lookup"><span data-stu-id="bfa24-112">Find Available Extensions</span></span>
<span data-ttu-id="bfa24-113">Puede buscar la extensión e información extendida con:</span><span class="sxs-lookup"><span data-stu-id="bfa24-113">You can locate extension and extended information using:</span></span>

* <span data-ttu-id="bfa24-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bfa24-114">PowerShell</span></span>
* <span data-ttu-id="bfa24-115">Interfaz de la línea de comandos entre plataformas de Azure (CLI de Azure)</span><span class="sxs-lookup"><span data-stu-id="bfa24-115">Azure Cross-Platform Command Line Interface (Azure CLI)</span></span>
* <span data-ttu-id="bfa24-116">API de REST de administración del servicio</span><span class="sxs-lookup"><span data-stu-id="bfa24-116">Service Management REST API</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="bfa24-117">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="bfa24-117">Azure PowerShell</span></span>
<span data-ttu-id="bfa24-118">Algunas extensiones tienen cmdlets de PowerShell que están toothem específico, que puede facilitar su configuración desde PowerShell; pero hello siguientes cmdlets funcionan para todas las extensiones de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bfa24-118">Some extensions have PowerShell cmdlets that are specific toothem, which may make their configuration from PowerShell easier; but hello following cmdlets work for all VM extensions.</span></span>

<span data-ttu-id="bfa24-119">Puede usar Hola siguiente cmdlets tooobtain información sobre las extensiones disponibles:</span><span class="sxs-lookup"><span data-stu-id="bfa24-119">You can use hello following cmdlets tooobtain information about available extensions:</span></span>

* <span data-ttu-id="bfa24-120">Para instancias de roles web o roles de trabajo, puede usar hello [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bfa24-120">For instances of web roles or worker roles, you can use hello [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet.</span></span>
* <span data-ttu-id="bfa24-121">Para instancias de máquinas virtuales, puede usar hello [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bfa24-121">For instances of Virtual Machines, you can use hello [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet.</span></span>
  
   <span data-ttu-id="bfa24-122">Hola, por ejemplo, el siguiente ejemplo de código muestra cómo toolist la información de hello **IaaSDiagnostics** extensión mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bfa24-122">For example, hello following code example shows how toolist the information for hello **IaaSDiagnostics** extension using PowerShell.</span></span>
  
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

### <a name="azure-command-line-interface-azure-cli"></a><span data-ttu-id="bfa24-123">Interfaz de la línea de comandos de Azure (CLI de Azure)</span><span class="sxs-lookup"><span data-stu-id="bfa24-123">Azure Command Line Interface (Azure CLI)</span></span>
<span data-ttu-id="bfa24-124">Algunas extensiones tienen comandos de CLI de Azure que están toothem específico (Hola extensión de máquina virtual de Docker es un ejemplo), que puede facilitar su configuración; pero los comandos del siguiente Hola todas las extensiones de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bfa24-124">Some extensions have Azure CLI commands that are specific toothem (hello Docker VM Extension is one example), which may make their configuration easier; but hello following commands work for all VM extensions.</span></span>

<span data-ttu-id="bfa24-125">Puede usar hello **lista de extensiones de máquina virtual de azure** comando tooobtain información sobre las extensiones disponibles y usar hello **–-json** opción toodisplay toda la información disponible acerca de una o varias extensiones.</span><span class="sxs-lookup"><span data-stu-id="bfa24-125">You can use hello **azure vm extension list** command tooobtain information about available extensions, and use hello **–-json** option toodisplay all available information about one or more extensions.</span></span> <span data-ttu-id="bfa24-126">Si no usa un nombre de extensión, comando hello devuelve una descripción de JSON de todas las extensiones disponibles.</span><span class="sxs-lookup"><span data-stu-id="bfa24-126">If you do not use an extension name, hello command returns a JSON description of all available extensions.</span></span>

<span data-ttu-id="bfa24-127">Por ejemplo, hello el ejemplo de código siguiente muestra cómo toolist Hola información de hello **IaaSDiagnostics** extensión con hello Azure CLI **lista de extensiones de máquina virtual de azure** comando y usos hello **–-json** opción tooreturn obtener información completa.</span><span class="sxs-lookup"><span data-stu-id="bfa24-127">For example, hello following code example shows how toolist hello information for hello **IaaSDiagnostics** extension using hello Azure CLI **azure vm extension list** command and uses hello **–-json** option tooreturn complete information.</span></span>

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



### <a name="service-management-rest-apis"></a><span data-ttu-id="bfa24-128">API de REST de administración de servicios</span><span class="sxs-lookup"><span data-stu-id="bfa24-128">Service Management REST APIs</span></span>
<span data-ttu-id="bfa24-129">Puede usar Hola siguiente las API de REST tooobtain información sobre las extensiones disponibles:</span><span class="sxs-lookup"><span data-stu-id="bfa24-129">You can use hello following REST APIs tooobtain information about available extensions:</span></span>

* <span data-ttu-id="bfa24-130">Para instancias de roles web o roles de trabajo, puede usar hello [enumerar extensiones disponibles](https://msdn.microsoft.com/library/dn169559.aspx) operación.</span><span class="sxs-lookup"><span data-stu-id="bfa24-130">For instances of web roles or worker roles, you can use hello [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span> <span data-ttu-id="bfa24-131">versiones de hello toolist de extensiones disponibles, puede usar [enumerar versiones de extensiones](https://msdn.microsoft.com/library/dn495437.aspx).</span><span class="sxs-lookup"><span data-stu-id="bfa24-131">toolist hello versions of available extensions, you can use [List Extension Versions](https://msdn.microsoft.com/library/dn495437.aspx).</span></span>
* <span data-ttu-id="bfa24-132">Para instancias de máquinas virtuales, puede usar hello [enumerar extensiones de recursos](https://msdn.microsoft.com/library/dn495441.aspx) operación.</span><span class="sxs-lookup"><span data-stu-id="bfa24-132">For instances of Virtual Machines, you can use hello [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span> <span data-ttu-id="bfa24-133">versiones de hello toolist de extensiones disponibles, puede usar [enumerar versiones de extensión de recursos](https://msdn.microsoft.com/library/dn495440.aspx).</span><span class="sxs-lookup"><span data-stu-id="bfa24-133">toolist hello versions of available extensions, you can use [List Resource Extension Versions](https://msdn.microsoft.com/library/dn495440.aspx).</span></span>

## <a name="add-update-or-disable-extensions"></a><span data-ttu-id="bfa24-134">Adición, actualización o deshabilitación de extensiones</span><span class="sxs-lookup"><span data-stu-id="bfa24-134">Add, Update, or Disable Extensions</span></span>
<span data-ttu-id="bfa24-135">Las extensiones se pueden agregar cuando se crea una instancia o se puede agregar tooa ejecuta la instancia.</span><span class="sxs-lookup"><span data-stu-id="bfa24-135">Extensions can be added when an instance is created or they can be added tooa running instance.</span></span> <span data-ttu-id="bfa24-136">Las extensiones se pueden actualizar, deshabilitar o quitar.</span><span class="sxs-lookup"><span data-stu-id="bfa24-136">Extensions can be updated, disabled, or removed.</span></span> <span data-ttu-id="bfa24-137">Puede realizar estas acciones mediante el uso de cmdlets de PowerShell de Azure o mediante operaciones de API de REST de administración de servicios de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfa24-137">You can perform these actions by using Azure PowerShell cmdlets or by using hello Service Management REST API operations.</span></span> <span data-ttu-id="bfa24-138">Parámetros necesario tooinstall y configuración algunas extensiones.</span><span class="sxs-lookup"><span data-stu-id="bfa24-138">Parameters are required tooinstall and set up some extensions.</span></span> <span data-ttu-id="bfa24-139">Se admiten parámetros públicos y privados con las extensiones.</span><span class="sxs-lookup"><span data-stu-id="bfa24-139">Public and private parameters are supported for extensions.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="bfa24-140">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="bfa24-140">Azure PowerShell</span></span>
<span data-ttu-id="bfa24-141">Uso de cmdlets de PowerShell de Azure es extensiones de manera más fáciles tooadd y actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfa24-141">Using Azure PowerShell cmdlets is hello easiest way tooadd and update extensions.</span></span> <span data-ttu-id="bfa24-142">Al usar cmdlets de extensión de hello, la mayor parte de la configuración de Hola de extensión de Hola se realiza automáticamente.</span><span class="sxs-lookup"><span data-stu-id="bfa24-142">When you use hello extension cmdlets, most of hello configuration of hello extension is done for you.</span></span> <span data-ttu-id="bfa24-143">En ocasiones, puede que necesite tooprogrammatically agregar una extensión.</span><span class="sxs-lookup"><span data-stu-id="bfa24-143">At times, you may need tooprogrammatically add an extension.</span></span> <span data-ttu-id="bfa24-144">Cuando necesite toodo esto, debe proporcionar la configuración de Hola de extensión de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfa24-144">When you need toodo this, you must provide hello configuration of hello extension.</span></span>

<span data-ttu-id="bfa24-145">Puede usar Hola después cmdlets tooknow si una extensión requiere una configuración de parámetros públicos o privados:</span><span class="sxs-lookup"><span data-stu-id="bfa24-145">You can use hello following cmdlets tooknow whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="bfa24-146">Para instancias de roles web o roles de trabajo, puede usar hello **Get-AzureServiceAvailableExtension** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bfa24-146">For instances of web roles or worker roles, you can use hello **Get-AzureServiceAvailableExtension** cmdlet.</span></span>
* <span data-ttu-id="bfa24-147">Para instancias de máquinas virtuales, puede usar hello **Get-AzureVMAvailableExtension** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bfa24-147">For instances of Virtual Machines, you can use hello **Get-AzureVMAvailableExtension** cmdlet.</span></span>

### <a name="service-management-rest-apis"></a><span data-ttu-id="bfa24-148">API de REST de administración de servicios</span><span class="sxs-lookup"><span data-stu-id="bfa24-148">Service Management REST APIs</span></span>
<span data-ttu-id="bfa24-149">Al recuperar una lista de extensiones disponibles mediante las API de REST de hello, recibirá información sobre cómo la extensión de hello toobe configurado.</span><span class="sxs-lookup"><span data-stu-id="bfa24-149">When you retrieve a listing of available extensions by using hello REST APIs, you receive information about how hello extension is toobe configured.</span></span> <span data-ttu-id="bfa24-150">información de Hola que se devuelve puede mostrar información sobre parámetros representada por un esquema público y privado.</span><span class="sxs-lookup"><span data-stu-id="bfa24-150">hello information that is returned might show parameter information represented by a public schema and private schema.</span></span> <span data-ttu-id="bfa24-151">Valores de parámetros públicos se devuelven en las consultas sobre las instancias de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfa24-151">Public parameter values are returned in queries about hello instances.</span></span> <span data-ttu-id="bfa24-152">No se devuelven los valores de parámetros privados.</span><span class="sxs-lookup"><span data-stu-id="bfa24-152">Private parameter values are not returned.</span></span>

<span data-ttu-id="bfa24-153">Puede usar Hola siguiendo las API de REST tooknow si una extensión requiere una configuración de parámetros públicos o privados:</span><span class="sxs-lookup"><span data-stu-id="bfa24-153">You can use hello following REST APIs tooknow whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="bfa24-154">Para instancias de roles web o roles de trabajo, Hola **PublicConfigurationSchema** y **PrivateConfigurationSchema** elementos contienen información de Hola en respuesta Hola Hola [lista Las extensiones disponibles](https://msdn.microsoft.com/library/dn169559.aspx) operación.</span><span class="sxs-lookup"><span data-stu-id="bfa24-154">For instances of web roles or worker roles, hello **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain hello information in hello response from hello [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span>
* <span data-ttu-id="bfa24-155">Para instancias de máquinas virtuales, Hola **PublicConfigurationSchema** y **PrivateConfigurationSchema** elementos contienen información de Hola en respuesta Hola Hola [lista Extensiones de recursos](https://msdn.microsoft.com/library/dn495441.aspx) operación.</span><span class="sxs-lookup"><span data-stu-id="bfa24-155">For instances of Virtual Machines, hello **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain hello information in hello response from hello [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span>

> [!NOTE]
> <span data-ttu-id="bfa24-156">Las extensiones también pueden usar configuraciones que se definen con JSON.</span><span class="sxs-lookup"><span data-stu-id="bfa24-156">Extensions can also use configurations that are defined with JSON.</span></span> <span data-ttu-id="bfa24-157">Cuando se utilizan estos tipos de extensiones, solo Hola **SampleConfig** elemento se utiliza.</span><span class="sxs-lookup"><span data-stu-id="bfa24-157">When these types of extensions are used, only hello **SampleConfig** element is used.</span></span>
> 
> 

