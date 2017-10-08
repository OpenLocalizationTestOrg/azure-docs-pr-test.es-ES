---
title: "aaaVariable activos de automatización de Azure | Documentos de Microsoft"
description: "Los activos de variable son valores que están disponibles tooall runbooks y las configuraciones de DSC en automatización de Azure.  En este artículo se explica los detalles de Hola de variables y cómo toowork con ellos en la creación gráfica y textual."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: b880c15f-46f5-4881-8e98-e034cc5a66ec
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/09/2017
ms.author: magoedte;bwren
ms.openlocfilehash: f9daa49fc1dc883ffb218a9adf26e36df1d6bb27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="variable-assets-in-azure-automation"></a><span data-ttu-id="c381b-104">Recursos de variables en Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="c381b-104">Variable assets in Azure Automation</span></span>

<span data-ttu-id="c381b-105">Los activos de variable son valores que están disponibles tooall runbooks y las configuraciones de DSC en su cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="c381b-105">Variable assets are values that are available tooall runbooks and DSC configurations in your automation account.</span></span> <span data-ttu-id="c381b-106">Puede crear, modificar y recuperar de hello portal de Azure, Windows PowerShell y desde un runbook o la configuración de DSC.</span><span class="sxs-lookup"><span data-stu-id="c381b-106">They can be created, modified, and retrieved from hello Azure portal, Windows PowerShell, and from within a runbook or DSC configuration.</span></span> <span data-ttu-id="c381b-107">Las variables de automatización son útiles para hello los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="c381b-107">Automation variables are useful for hello following scenarios:</span></span>

- <span data-ttu-id="c381b-108">Compartir un valor entre varios runbooks o configuraciones de DSC.</span><span class="sxs-lookup"><span data-stu-id="c381b-108">Share a value between multiple runbooks or DSC configurations.</span></span>

- <span data-ttu-id="c381b-109">Compartir un valor entre varios trabajos de hello mismo runbook o configuración de DSC.</span><span class="sxs-lookup"><span data-stu-id="c381b-109">Share a value between multiple jobs from hello same runbook or DSC configuration.</span></span>

- <span data-ttu-id="c381b-110">Administrar un valor desde el portal de Hola o de línea de comandos de Windows PowerShell de Hola que usa runbooks o configuraciones de DSC, como un conjunto de elementos de configuración comunes como lista específica de los nombres de las VM, un grupo de recursos específico, un nombre de dominio de AD, etcetera.</span><span class="sxs-lookup"><span data-stu-id="c381b-110">Manage a value from hello portal or from hello Windows PowerShell command line that is used by runbooks or DSC configurations, such as a set of common configuration items like specific list of VM names, a specific resource group,  an AD domain name, etc.</span></span>  

<span data-ttu-id="c381b-111">Las variables de automatización se conservan para que sigan toobe disponible incluso si se produce un error en el runbook de Hola o configuración de DSC.</span><span class="sxs-lookup"><span data-stu-id="c381b-111">Automation variables are persisted so that they continue toobe available even if hello runbook or DSC configuration fails.</span></span>  <span data-ttu-id="c381b-112">Esto también permite un toobe valor establecido por un runbook que, a continuación, se utiliza por otro, o usa Hola mismo runbook o hello de configuración de DSC próxima vez que se ejecute.</span><span class="sxs-lookup"><span data-stu-id="c381b-112">This also allows a value toobe set by one runbook that is then used by another, or is used by hello same runbook or DSC configuration hello next time that it is run.</span></span>

<span data-ttu-id="c381b-113">Cuando se crea una variable, puede especificar que se almacene cifrada.</span><span class="sxs-lookup"><span data-stu-id="c381b-113">When a variable is created, you can specify that it be stored encrypted.</span></span>  <span data-ttu-id="c381b-114">Cuando se cifra una variable, se almacenan de forma segura en automatización de Azure y su valor no se puede recuperar de hello [AzureRmAutomationVariable Get](https://msdn.microsoft.com/library/mt603849.aspx) cmdlet que se suministra como parte del módulo de PowerShell de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="c381b-114">When a variable is encrypted, it is stored securely in Azure Automation, and its value cannot be retrieved from hello [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) cmdlet that ships as part of hello Azure PowerShell module.</span></span>  <span data-ttu-id="c381b-115">Hello única manera que se puede recuperar un valor cifrado es con hello **Get-AutomationVariable** actividad en un runbook o la configuración de DSC.</span><span class="sxs-lookup"><span data-stu-id="c381b-115">hello only way that an encrypted value can be retrieved is from hello **Get-AutomationVariable** activity in a runbook or DSC configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="c381b-116">Los recursos protegidos en Automatización de Azure incluyen credenciales, certificados, conexiones y variables cifradas.</span><span class="sxs-lookup"><span data-stu-id="c381b-116">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="c381b-117">Estos activos se cifran y almacenan en hello automatización de Azure mediante una clave única que se genera para cada cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="c381b-117">These assets are encrypted and stored in hello Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="c381b-118">Esta clave se cifra mediante un certificado maestro y se almacena en Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="c381b-118">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="c381b-119">Antes de almacenar un recurso seguro, clave de hello para la cuenta de automatización de Hola se descifra mediante certificado maestro hello y, a continuación, utilice activos de hello tooencrypt.</span><span class="sxs-lookup"><span data-stu-id="c381b-119">Before storing a secure asset, hello key for hello automation account is decrypted using hello master certificate and then used tooencrypt hello asset.</span></span>

## <a name="variable-types"></a><span data-ttu-id="c381b-120">Tipos de variables</span><span class="sxs-lookup"><span data-stu-id="c381b-120">Variable types</span></span>

<span data-ttu-id="c381b-121">Cuando se crea una variable con hello portal de Azure, debe especificar un tipo de datos de la lista desplegable de hello para que el portal de hello puede mostrar el control adecuado de Hola para escribir el valor de la variable Hola.</span><span class="sxs-lookup"><span data-stu-id="c381b-121">When you create a variable with hello Azure portal, you must specify a data type from hello drop-down list so hello portal can display hello appropriate control for entering hello variable value.</span></span> <span data-ttu-id="c381b-122">Hola variable no está restringido toothis datos tipo, pero debe establecer variable de hello mediante Windows PowerShell si desea toospecify un valor de un tipo diferente.</span><span class="sxs-lookup"><span data-stu-id="c381b-122">hello variable is not restricted toothis data type, but you must set hello variable using Windows PowerShell if you want toospecify a value of a different type.</span></span> <span data-ttu-id="c381b-123">Si especifica **no definido**, valor de Hola de variable de saludo se establecerá demasiado**$null**, y se debe establecer el valor de hello con hello [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet o **Set-AutomationVariable** actividad.</span><span class="sxs-lookup"><span data-stu-id="c381b-123">If you specify **Not defined**, then hello value of hello variable will be set too**$null**, and you must set hello value with hello [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet or **Set-AutomationVariable** activity.</span></span>  <span data-ttu-id="c381b-124">No se puede crear o cambiar el valor de Hola para un tipo complejo de variable en el portal de Hola, pero puede proporcionar un valor de cualquier tipo de uso de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c381b-124">You cannot create or change hello value for a complex variable type in hello portal, but you can provide a value of any type using Windows PowerShell.</span></span> <span data-ttu-id="c381b-125">Los tipos complejos se devolverán como un [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).</span><span class="sxs-lookup"><span data-stu-id="c381b-125">Complex types will be returned as a [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).</span></span>

<span data-ttu-id="c381b-126">Puede almacenar varios valores tooa variable de tipo simple mediante la creación de una matriz o tabla hash y guardarlo toohello variable.</span><span class="sxs-lookup"><span data-stu-id="c381b-126">You can store multiple values tooa single variable by creating an array or hashtable and saving it toohello variable.</span></span>

<span data-ttu-id="c381b-127">siguiente Hola es una lista de tipos de variable de automatización:</span><span class="sxs-lookup"><span data-stu-id="c381b-127">hello following are a list of variable types available in Automation:</span></span>

* <span data-ttu-id="c381b-128">String</span><span class="sxs-lookup"><span data-stu-id="c381b-128">String</span></span>
* <span data-ttu-id="c381b-129">Entero </span><span class="sxs-lookup"><span data-stu-id="c381b-129">Integer</span></span>
* <span data-ttu-id="c381b-130">DateTime</span><span class="sxs-lookup"><span data-stu-id="c381b-130">DateTime</span></span>
* <span data-ttu-id="c381b-131">Booleano</span><span class="sxs-lookup"><span data-stu-id="c381b-131">Boolean</span></span>
* <span data-ttu-id="c381b-132">Null</span><span class="sxs-lookup"><span data-stu-id="c381b-132">Null</span></span>

## <a name="cmdlets-and-workflow-activities"></a><span data-ttu-id="c381b-133">Cmdlets y actividades de flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="c381b-133">Cmdlets and workflow activities</span></span>

<span data-ttu-id="c381b-134">cmdlets de Hello en hello en la tabla siguiente son toocreate usado y administrar variables de automatización con Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c381b-134">hello cmdlets in hello following table are used toocreate and manage Automation variables with Windows PowerShell.</span></span> <span data-ttu-id="c381b-135">Se incluyen como parte del programa Hola a [módulo Azure PowerShell](../powershell-install-configure.md) que está disponible para su uso en runbooks de automatización y la configuración de DSC.</span><span class="sxs-lookup"><span data-stu-id="c381b-135">They ship as part of hello [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configuration.</span></span>

|<span data-ttu-id="c381b-136">Cmdlets</span><span class="sxs-lookup"><span data-stu-id="c381b-136">Cmdlets</span></span>|<span data-ttu-id="c381b-137">Descripción</span><span class="sxs-lookup"><span data-stu-id="c381b-137">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="c381b-138">Get-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="c381b-138">Get-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603849.aspx)|<span data-ttu-id="c381b-139">Recupera el valor de Hola de una variable existente.</span><span class="sxs-lookup"><span data-stu-id="c381b-139">Retrieves hello value of an existing variable.</span></span>|
|[<span data-ttu-id="c381b-140">New-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="c381b-140">New-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603613.aspx)|<span data-ttu-id="c381b-141">Crea una nueva variable y establece su valor.</span><span class="sxs-lookup"><span data-stu-id="c381b-141">Creates a new variable and sets its value.</span></span>|
|[<span data-ttu-id="c381b-142">Remove-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="c381b-142">Remove-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt619354.aspx)|<span data-ttu-id="c381b-143">Quita una variable existente.</span><span class="sxs-lookup"><span data-stu-id="c381b-143">Removes an existing variable.</span></span>|
|[<span data-ttu-id="c381b-144">Set-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="c381b-144">Set-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603601.aspx)|<span data-ttu-id="c381b-145">Establece el valor de Hola de una variable existente.</span><span class="sxs-lookup"><span data-stu-id="c381b-145">Sets hello value for an existing variable.</span></span>|

<span data-ttu-id="c381b-146">las actividades de flujo de trabajo de Hello en hello en la tabla siguiente son tooaccess usa las variables de automatización en un runbook.</span><span class="sxs-lookup"><span data-stu-id="c381b-146">hello workflow activities in hello following table are used tooaccess Automation variables in a runbook.</span></span> <span data-ttu-id="c381b-147">Que solo están disponibles para su uso en un runbook o la configuración de DSC y no se incluyen como parte del módulo de PowerShell de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="c381b-147">They are only available for use in a runbook or DSC configuration, and do not ship as part of hello Azure PowerShell module.</span></span>

|<span data-ttu-id="c381b-148">Actividades de flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="c381b-148">Workflow Activities</span></span>|<span data-ttu-id="c381b-149">Description</span><span class="sxs-lookup"><span data-stu-id="c381b-149">Description</span></span>|
|:---|:---|
|<span data-ttu-id="c381b-150">Get-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="c381b-150">Get-AutomationVariable</span></span>|<span data-ttu-id="c381b-151">Recupera el valor de Hola de una variable existente.</span><span class="sxs-lookup"><span data-stu-id="c381b-151">Retrieves hello value of an existing variable.</span></span>|
|<span data-ttu-id="c381b-152">Set-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="c381b-152">Set-AutomationVariable</span></span>|<span data-ttu-id="c381b-153">Establece el valor de Hola de una variable existente.</span><span class="sxs-lookup"><span data-stu-id="c381b-153">Sets hello value for an existing variable.</span></span>|

> [!NOTE] 
> <span data-ttu-id="c381b-154">Debe evitar usar variables en Hola: parámetro de nombre de **Get-AutomationVariable** en un runbook o la configuración de DSC, ya que esto puede complicar la detección de dependencias entre runbooks o la configuración de DSC y la automatización variables en tiempo de diseño.</span><span class="sxs-lookup"><span data-stu-id="c381b-154">You should avoid using variables in hello –Name parameter of **Get-AutomationVariable**  in a runbook or DSC configuration since this can complicate discovering dependencies between runbooks or DSC configuration, and Automation variables at design time.</span></span>

## <a name="creating-a-new-automation-variable"></a><span data-ttu-id="c381b-155">Creación de una nueva variable de Automatización</span><span class="sxs-lookup"><span data-stu-id="c381b-155">Creating a new Automation variable</span></span>

### <a name="toocreate-a-new-variable-with-hello-azure-portal"></a><span data-ttu-id="c381b-156">toocreate una nueva variable con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c381b-156">toocreate a new variable with hello Azure portal</span></span>

1. <span data-ttu-id="c381b-157">En su cuenta de automatización, haga clic en hello **activos** icono y, a continuación, en hello **activos** hoja, seleccione **Variables**.</span><span class="sxs-lookup"><span data-stu-id="c381b-157">From your Automation account, click hello **Assets** tile and then on hello **Assets** blade, select **Variables**.</span></span>
2. <span data-ttu-id="c381b-158">En hello **Variables** , seleccione **agregar una variable**.</span><span class="sxs-lookup"><span data-stu-id="c381b-158">On hello **Variables** tile, select **Add a variable**.</span></span>
3. <span data-ttu-id="c381b-159">Complete las opciones de hello en hello **nueva Variable** hoja y haga clic en **crear** guardar Hola nueva variable.</span><span class="sxs-lookup"><span data-stu-id="c381b-159">Complete hello options on hello **New Variable** blade and click **Create** save hello new variable.</span></span>

### <a name="toocreate-a-new-variable-with-windows-powershell"></a><span data-ttu-id="c381b-160">toocreate una nueva variable con Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="c381b-160">toocreate a new variable with Windows PowerShell</span></span>

<span data-ttu-id="c381b-161">Hola [AzureRmAutomationVariable New](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet crea una nueva variable y establece su valor inicial.</span><span class="sxs-lookup"><span data-stu-id="c381b-161">hello [New-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet creates a new variable and sets its initial value.</span></span> <span data-ttu-id="c381b-162">Se puede recuperar el valor de hello mediante [AzureRmAutomationVariable Get](https://msdn.microsoft.com/library/mt603849.aspx).</span><span class="sxs-lookup"><span data-stu-id="c381b-162">You can retrieve hello value using [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx).</span></span> <span data-ttu-id="c381b-163">Si el valor de hello es un tipo simple, se devuelve ese mismo tipo.</span><span class="sxs-lookup"><span data-stu-id="c381b-163">If hello value is a simple type, then that same type is returned.</span></span> <span data-ttu-id="c381b-164">Si es un tipo complejo, se devuelve **PSCustomObject** .</span><span class="sxs-lookup"><span data-stu-id="c381b-164">If it’s a complex type, then a **PSCustomObject** is returned.</span></span>

<span data-ttu-id="c381b-165">Mostrar comandos de ejemplo siguiente Hola cómo toocreate una variable de tipo cadena y, a continuación, devolver su valor.</span><span class="sxs-lookup"><span data-stu-id="c381b-165">hello following sample commands show how toocreate a variable of type string and then return its value.</span></span>

    New-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" 
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable' `
    –Encrypted $false –Value 'My String'
    $string = (Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable').Value

<span data-ttu-id="c381b-166">Mostrar comandos de ejemplo siguiente Hola cómo toocreate una variable con un complejo escriba y, a continuación, devolver sus propiedades.</span><span class="sxs-lookup"><span data-stu-id="c381b-166">hello following sample commands show how toocreate a variable with a complex type and then return its properties.</span></span> <span data-ttu-id="c381b-167">En este caso, se usa un objeto de máquina virtual desde **Get-AzureRmVm**.</span><span class="sxs-lookup"><span data-stu-id="c381b-167">In this case, a virtual machine object from **Get-AzureRmVm** is used.</span></span>

    $vm = Get-AzureRmVm -ResourceGroupName "ResourceGroup01" –Name "VM01"
    New-AzureRmAutomationVariable –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable" –Encrypted $false –Value $vm
    
    $vmValue = (Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable").Value
    $vmName = $vmValue.Name
    $vmIpAddress = $vmValue.IpAddress



## <a name="using-a-variable-in-a-runbook-or-dsc-configuration"></a><span data-ttu-id="c381b-168">Uso de una variable en un runbook o una configuración de DSC</span><span class="sxs-lookup"><span data-stu-id="c381b-168">Using a variable in a runbook or DSC configuration</span></span>

<span data-ttu-id="c381b-169">Hola de uso **Set-AutomationVariable** valores de hello tooset las actividades de una variable de automatización en un runbook o configuración de DSC, hello y **Get-AutomationVariable** tooretrieve lo.</span><span class="sxs-lookup"><span data-stu-id="c381b-169">Use hello **Set-AutomationVariable** activity tooset hello value of an Automation variable in a runbook or DSC configuration, and hello **Get-AutomationVariable** tooretrieve it.</span></span>  <span data-ttu-id="c381b-170">No debe usar hello **Set-AzureAutomationVariable** o **Get-AzureAutomationVariable** cmdlets en un runbook o la configuración de DSC, ya que son menos eficientes que las actividades de flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c381b-170">You shouldn't use hello **Set-AzureAutomationVariable** or  **Get-AzureAutomationVariable** cmdlets in a runbook or DSC configuration since they are less efficient than hello workflow activities.</span></span>  <span data-ttu-id="c381b-171">No se puede recuperar también valor Hola de variables seguras con **Get-AzureAutomationVariable**.</span><span class="sxs-lookup"><span data-stu-id="c381b-171">You also cannot retrieve hello value of secure variables with **Get-AzureAutomationVariable**.</span></span>  <span data-ttu-id="c381b-172">Hola toocreate de manera solo una variable desde dentro de un runbook o la configuración de DSC es hello toouse [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c381b-172">hello only way toocreate a new variable from within a runbook or DSC configuration is toouse hello [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx)  cmdlet.</span></span>


### <a name="textual-runbook-samples"></a><span data-ttu-id="c381b-173">Ejemplos de runbook textual</span><span class="sxs-lookup"><span data-stu-id="c381b-173">Textual runbook samples</span></span>

#### <a name="setting-and-retrieving-a-simple-value-from-a-variable"></a><span data-ttu-id="c381b-174">Establecimiento y recuperación de un valor simple de una variable</span><span class="sxs-lookup"><span data-stu-id="c381b-174">Setting and retrieving a simple value from a variable</span></span>

<span data-ttu-id="c381b-175">Mostrar comandos de ejemplo siguiente Hola cómo tooset y recuperar una variable en un runbook textual.</span><span class="sxs-lookup"><span data-stu-id="c381b-175">hello following sample commands show how tooset and retrieve a variable in a textual runbook.</span></span> <span data-ttu-id="c381b-176">En este ejemplo, se asume que se crearon las variables de tipo entero llamadas *NumberOfIterations* y *NumberOfRunnings* y una variable de tipo cadena denominada *SampleMessage*.</span><span class="sxs-lookup"><span data-stu-id="c381b-176">In this sample, it is assumed that variables of type integer named *NumberOfIterations* and *NumberOfRunnings* and a variable of type string named *SampleMessage* have already been created.</span></span>

    $NumberOfIterations = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfIterations'
    $NumberOfRunnings = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfRunnings'
    $SampleMessage = Get-AutomationVariable -Name 'SampleMessage'
    
    Write-Output "Runbook has been run $NumberOfRunnings times."
    
    for ($i = 1; $i -le $NumberOfIterations; $i++) {
       Write-Output "$i`: $SampleMessage"
    }
    Set-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" –Name NumberOfRunnings –Value ($NumberOfRunnings += 1)

#### <a name="setting-and-retrieving-a-complex-object-in-a-variable"></a><span data-ttu-id="c381b-177">Establecimiento y recuperación de un objeto completo en una variable</span><span class="sxs-lookup"><span data-stu-id="c381b-177">Setting and retrieving a complex object in a variable</span></span>

<span data-ttu-id="c381b-178">siguiente Hola código de ejemplo muestra cómo tooupdate una variable con un valor complejo en un runbook textual.</span><span class="sxs-lookup"><span data-stu-id="c381b-178">hello following sample code shows how tooupdate a variable with a complex value in a textual runbook.</span></span> <span data-ttu-id="c381b-179">En este ejemplo, se recupera una máquina virtual de Azure con **Get-AzureVM** y guardado tooan variable de automatización existente.</span><span class="sxs-lookup"><span data-stu-id="c381b-179">In this sample, an Azure virtual machine is retrieved with **Get-AzureVM** and saved tooan existing Automation variable.</span></span>  <span data-ttu-id="c381b-180">Como se explica en [Tipos de variables](#variable-types), se almacena como un PSCustomObject.</span><span class="sxs-lookup"><span data-stu-id="c381b-180">As explained in [Variable types](#variable-types), this is stored as a PSCustomObject.</span></span>

    $vm = Get-AzureVM -ServiceName "MyVM" -Name "MyVM"
    Set-AutomationVariable -Name "MyComplexVariable" -Value $vm


<span data-ttu-id="c381b-181">En el siguiente código de hello, el valor de Hola se recupera de la máquina virtual de hello toostart variable y usar Hola.</span><span class="sxs-lookup"><span data-stu-id="c381b-181">In hello following code, hello value is retrieved from hello variable and used toostart hello virtual machine.</span></span>

    $vmObject = Get-AutomationVariable -Name "MyComplexVariable"
    if ($vmObject.PowerState -eq 'Stopped') {
       Start-AzureVM -ServiceName $vmObject.ServiceName -Name $vmObject.Name
    }


#### <a name="setting-and-retrieving-a-collection-in-a-variable"></a><span data-ttu-id="c381b-182">Establecimiento y recuperación de una colección en una variable</span><span class="sxs-lookup"><span data-stu-id="c381b-182">Setting and retrieving a collection in a variable</span></span>

<span data-ttu-id="c381b-183">siguiente Hola código de ejemplo muestra cómo toouse una variable con una colección de valores complejos en un runbook textual.</span><span class="sxs-lookup"><span data-stu-id="c381b-183">hello following sample code shows how toouse a variable with a collection of complex values in a textual runbook.</span></span> <span data-ttu-id="c381b-184">En este ejemplo, se recuperan varias máquinas virtuales de Azure con **Get-AzureVM** y guardado tooan variable de automatización existente.</span><span class="sxs-lookup"><span data-stu-id="c381b-184">In this sample, multiple Azure virtual machines are retrieved with **Get-AzureVM** and saved tooan existing Automation variable.</span></span>  <span data-ttu-id="c381b-185">Como se explica en [Tipos de variables](#variable-types), se almacena como una colección de objetos PSCustomObject.</span><span class="sxs-lookup"><span data-stu-id="c381b-185">As explained in [Variable types](#variable-types), this is stored as a collection of PSCustomObjects.</span></span>

    $vms = Get-AzureVM | Where -FilterScript {$_.Name -match "my"}     
    Set-AutomationVariable -Name 'MyComplexVariable' -Value $vms

<span data-ttu-id="c381b-186">En el siguiente código de hello, colección de Hola se recupera de la variable de Hola y toostart usa cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c381b-186">In hello following code, hello collection is retrieved from hello variable and used toostart each virtual machine.</span></span>

    $vmValues = Get-AutomationVariable -Name "MyComplexVariable"
    ForEach ($vmValue in $vmValues)
    {
       if ($vmValue.PowerState -eq 'Stopped') {
          Start-AzureVM -ServiceName $vmValue.ServiceName -Name $vmValue.Name
       }
    }


### <a name="graphical-runbook-samples"></a><span data-ttu-id="c381b-187">Ejemplos de runbook gráfico</span><span class="sxs-lookup"><span data-stu-id="c381b-187">Graphical runbook samples</span></span>

<span data-ttu-id="c381b-188">En un runbook gráfico, agregar hello **Get-AutomationVariable** o **Set-AutomationVariable** , haga doble clic en la variable de hello en panel de la biblioteca de Hola de editor gráfico de Hola y seleccione Hola actividad que desee.</span><span class="sxs-lookup"><span data-stu-id="c381b-188">In a graphical runbook, you add hello **Get-AutomationVariable** or **Set-AutomationVariable** by right-clicking on hello variable in hello Library pane of hello graphical editor and selecting hello activity you want.</span></span>

![Agregar variable toocanvas](media/automation-variables/runbook-variable-add-canvas.png)

#### <a name="setting-values-in-a-variable"></a><span data-ttu-id="c381b-190">Configuración de valores de una variable</span><span class="sxs-lookup"><span data-stu-id="c381b-190">Setting values in a variable</span></span>
<span data-ttu-id="c381b-191">Hello siguiente imagen muestra ejemplo actividades tooupdate una variable con un valor simple en un runbook gráfico.</span><span class="sxs-lookup"><span data-stu-id="c381b-191">hello following image shows sample activities tooupdate a variable with a simple value in a graphical runbook.</span></span> <span data-ttu-id="c381b-192">En este ejemplo, se recupera una sola máquina virtual de Azure con **AzureRmVM Get** y el nombre del equipo de Hola se guarda tooan variable de automatización existente con un tipo de cadena.</span><span class="sxs-lookup"><span data-stu-id="c381b-192">In this sample, a single Azure virtual machine is retrieved with **Get-AzureRmVM** and hello computer name is saved tooan existing Automation variable with a type of String.</span></span>  <span data-ttu-id="c381b-193">No importa si hello [vínculo es una canalización o una secuencia](automation-graphical-authoring-intro.md#links-and-workflow) ya que solo se puede esperar un único objeto de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="c381b-193">It doesn't matter whether hello [link is a pipeline or sequence](automation-graphical-authoring-intro.md#links-and-workflow) since we only expect a single object in hello output.</span></span>

![Establecimiento de una variable simple](media/automation-variables/runbook-set-simple-variable.png)

## <a name="next-steps"></a><span data-ttu-id="c381b-195">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c381b-195">Next Steps</span></span>

* <span data-ttu-id="c381b-196">toolearn más acerca de cómo conectar actividades juntos en el gráfico de creación, vea [vínculos de edición gráfica](automation-graphical-authoring-intro.md#links-and-workflow)</span><span class="sxs-lookup"><span data-stu-id="c381b-196">toolearn more about connecting activities together in graphical authoring, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow)</span></span>
* <span data-ttu-id="c381b-197">tooget a trabajar con runbooks gráficos, consulte [mi primer runbook gráfico](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="c381b-197">tooget started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span> 

