---
title: "aaaCreate un módulo de integración de la automatización de Azure | Documentos de Microsoft"
description: "Tutorial le guía a través del uso de creación, las pruebas y ejemplo de Hola de módulos de integración en automatización de Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 27798efb-08b9-45d9-9b41-5ad91a3df41e
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/13/2017
ms.author: magoedte
ms.openlocfilehash: d4064d8b106496f4dab442024131886c4affccab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-integration-modules"></a><span data-ttu-id="1bc04-103">Módulos de integración de Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="1bc04-103">Azure Automation Integration Modules</span></span>
<span data-ttu-id="1bc04-104">PowerShell es tecnología fundamental de hello detrás de automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="1bc04-104">PowerShell is hello fundamental technology behind Azure Automation.</span></span> <span data-ttu-id="1bc04-105">Dado que la automatización de Azure se basa en PowerShell, los módulos de PowerShell son extensibilidad toohello clave de automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="1bc04-105">Since Azure Automation is built on PowerShell, PowerShell modules are key toohello extensibility of Azure Automation.</span></span> <span data-ttu-id="1bc04-106">En este artículo, se le ayudará a obtener información específica de Hola de uso de automatización de Azure de módulos de PowerShell, denominada tooas "Módulos de integración" y las prácticas recomendadas para crear su propio toomake de módulos de PowerShell que funcionan como módulos de integración en Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="1bc04-106">In this article, we will guide you through hello specifics of Azure Automation’s use of PowerShell modules, referred tooas “Integration Modules”, and best practices for creating your own PowerShell modules toomake sure they work as Integration Modules within Azure Automation.</span></span> 

## <a name="what-is-a-powershell-module"></a><span data-ttu-id="1bc04-107">¿Qué son los módulos de PowerShell?</span><span class="sxs-lookup"><span data-stu-id="1bc04-107">What is a PowerShell Module?</span></span>
<span data-ttu-id="1bc04-108">Un módulo de PowerShell es un grupo de cmdlets de PowerShell como **Get-Date** o **Copy-Item**que puede utilizarse desde la consola de PowerShell de hello, scripts, flujos de trabajo, runbooks y, al igual que los recursos de DSC de PowerShell WindowsFeature o archivo, que puede usarse desde configuraciones de DSC de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1bc04-108">A PowerShell module is a group of PowerShell cmdlets like **Get-Date** or **Copy-Item**, that can be used from hello PowerShell console, scripts, workflows, runbooks, and PowerShell DSC resources like WindowsFeature or File, that can be used from PowerShell DSC configurations.</span></span> <span data-ttu-id="1bc04-109">Toda la funcionalidad de Hola de PowerShell se expone a través de los cmdlets y recursos de DSC y cada recurso de DSC de cmdlet/está respaldado por un módulo de PowerShell, muchos de los que se suministran con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1bc04-109">All of hello functionality of PowerShell is exposed through cmdlets and DSC resources, and every cmdlet/DSC resource is backed by a PowerShell module, many of which ship with PowerShell itself.</span></span> <span data-ttu-id="1bc04-110">Por ejemplo, hello **Get-Date** cmdlet forma parte del programa Hola módulo Microsoft.PowerShell.Utility PowerShell, y **Copy-Item** cmdlet forma parte del módulo Microsoft.PowerShell.Management PowerShell hello y Hola recurso de DSC de paquete forma parte del módulo PSDesiredStateConfiguration PowerShell Hola.</span><span class="sxs-lookup"><span data-stu-id="1bc04-110">For example, hello **Get-Date** cmdlet is part of hello Microsoft.PowerShell.Utility PowerShell module, and **Copy-Item** cmdlet is part of hello Microsoft.PowerShell.Management PowerShell module and hello Package DSC resource is part of hello PSDesiredStateConfiguration PowerShell module.</span></span> <span data-ttu-id="1bc04-111">Estos módulos se suministran con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1bc04-111">Both of these modules ship with PowerShell.</span></span> <span data-ttu-id="1bc04-112">Sin embargo, muchos módulos de PowerShell no se incluyen como parte de PowerShell y en su lugar se distribuyen con productos de primer o terceros como System Center 2012 Configuration Manager o amplia comunidad de PowerShell hello en lugares como galería de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1bc04-112">But many PowerShell modules do not ship as part of PowerShell, and are instead distributed with first or third-party products like System Center 2012 Configuration Manager or by hello vast PowerShell community on places like PowerShell Gallery.</span></span>  <span data-ttu-id="1bc04-113">módulos de Hello son útiles porque simplifican las tareas complejas más sencilla a través de la funcionalidad encapsulada.</span><span class="sxs-lookup"><span data-stu-id="1bc04-113">hello modules are useful because they make complex tasks simpler through encapsulated functionality.</span></span>  <span data-ttu-id="1bc04-114">Puede obtener más información sobre los [módulos de PowerShell en MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="1bc04-114">You can learn more about [PowerShell modules on MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx).</span></span> 

## <a name="what-is-an-azure-automation-integration-module"></a><span data-ttu-id="1bc04-115">¿Qué son los módulos de integración de Automatización de Azure?</span><span class="sxs-lookup"><span data-stu-id="1bc04-115">What is an Azure Automation Integration Module?</span></span>
<span data-ttu-id="1bc04-116">Los módulos de integración se parecen mucho a los módulos de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1bc04-116">An Integration Module isn't very different from a PowerShell module.</span></span> <span data-ttu-id="1bc04-117">Su simplemente un módulo de PowerShell que contiene opcionalmente un archivo adicional: un archivo de metadatos especificando un toobe del tipo de conexión de automatización de Azure usado con los cmdlets del módulo de hello en runbooks.</span><span class="sxs-lookup"><span data-stu-id="1bc04-117">Its simply a PowerShell module that optionally contains one additional file - a metadata file specifying an Azure Automation connection type toobe used with hello module's cmdlets in runbooks.</span></span> <span data-ttu-id="1bc04-118">Opcional de archivos o no, estos módulos se importan en toomake de automatización de Azure sus cmdlets disponibles para usar en runbooks y sus recursos de DSC disponibles para su uso en las configuraciones de DSC de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1bc04-118">Optional file or not, these PowerShell modules can be imported into Azure Automation toomake their cmdlets available for use within runbooks and their DSC resources available for use within DSC configurations.</span></span> <span data-ttu-id="1bc04-119">Entre bastidores de hello, automatización de Azure almacena estos módulos y en el trabajo del runbook y tiempo de ejecución de trabajo de compilación DSC, los carga en espacios aislados de automatización de Azure de Hola donde se ejecutan los runbooks y las configuraciones de DSC se compilan.</span><span class="sxs-lookup"><span data-stu-id="1bc04-119">Behind hello scenes, Azure Automation stores these modules, and at runbook job and DSC compilation job execution time, loads them into hello Azure Automation sandboxes where runbooks are executed and DSC configurations are compiled.</span></span>  <span data-ttu-id="1bc04-120">Los recursos de DSC en los módulos se colocan también automáticamente en el servidor de extracción de DSC de automatización de hello, para que pueden extraerse máquinas intentar tooapply las configuraciones de DSC.</span><span class="sxs-lookup"><span data-stu-id="1bc04-120">Any DSC resources in modules are also automatically placed on hello Automation DSC pull server, so that they can be pulled by machines attempting tooapply DSC configurations.</span></span>  

<span data-ttu-id="1bc04-121">Enviamos un número de módulos de PowerShell de Azure fuera del cuadro hello en automatización de Azure para toouse, por lo que puede empezar a automatizar la administración de Azure inmediatamente, pero puede importar módulos de PowerShell para cualquier sistema, el servicio o la herramienta que desee toointegrate con.</span><span class="sxs-lookup"><span data-stu-id="1bc04-121">We ship a number of Azure  PowerShell modules out of hello box in Azure Automation for you toouse so you can get started automating Azure management right away, but you can import PowerShell modules for whatever system, service, or tool you want toointegrate with.</span></span> 

> [!NOTE]
> <span data-ttu-id="1bc04-122">Algunos módulos se incluyen como "módulos globales" en el servicio de automatización de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bc04-122">Certain modules are shipped as “global modules” in hello Automation service.</span></span> <span data-ttu-id="1bc04-123">Estos módulos globales están disponible tooyou cuando se crea una cuenta de automatización, y se actualice a veces, que envía automáticamente tooyour cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="1bc04-123">These global modules are available tooyou when you create an automation account, and we update them sometimes which automatically pushes them out tooyour automation account.</span></span> <span data-ttu-id="1bc04-124">Si no desea toobe actualizadas de forma automática, siempre puede importar Hola mismo módulo usted mismo y que tendrá prioridad sobre la versión de módulo global Hola de ese módulo que se incluyen en el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bc04-124">If you don’t want them toobe auto-updated, you can always import hello same module yourself, and that will take precedence over hello global module version of that module that we ship in hello service.</span></span> 

<span data-ttu-id="1bc04-125">formato de Hello en el que importar un paquete de módulo de integración es un archivo comprimido con el mismo nombre que el módulo de hello y una extensión .zip de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bc04-125">hello format in which you import an Integration Module package is a compressed file with hello same name as hello module and a .zip extension.</span></span> <span data-ttu-id="1bc04-126">Que contiene el módulo de Windows PowerShell de Hola y los archivos auxiliares, incluido un archivo de manifiesto (. psd1) si el módulo de hello tiene uno.</span><span class="sxs-lookup"><span data-stu-id="1bc04-126">It contains hello Windows PowerShell module and any supporting files, including a manifest file (.psd1) if hello module has one.</span></span>

<span data-ttu-id="1bc04-127">Si el módulo de hello debe contener un tipo de conexión de automatización de Azure, también debe contener un archivo con nombre hello `<ModuleName>-Automation.json` que especifica las propiedades de tipo de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bc04-127">If hello module should contain an Azure Automation connection type, it must also contain a file with hello name `<ModuleName>-Automation.json` that specifies hello connection type properties.</span></span> <span data-ttu-id="1bc04-128">Esto es un archivo json que se coloca dentro de la carpeta del módulo de hello del archivo .zip comprimido y contienen campos de Hola de una "conexión" que es necesario tooconnect toohello sistema o servicio Hola módulo representa.</span><span class="sxs-lookup"><span data-stu-id="1bc04-128">This is a json file placed within hello module folder of your compressed .zip file, and contains hello fields of a “connection” that is required tooconnect toohello system or service hello module represents.</span></span> <span data-ttu-id="1bc04-129">De este modo, se creará un tipo de conexión en Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="1bc04-129">This will end up creating a connection type in Azure Automation.</span></span> <span data-ttu-id="1bc04-130">Uso de este archivo se puede establecer los nombres de campo de hello, tipos, y si deben ser campos Hola cifrados u opcional para el tipo de conexión de hello del módulo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bc04-130">Using this file you can set hello field names, types, and whether hello fields should be encrypted and / or optional, for hello connection type of hello module.</span></span> <span data-ttu-id="1bc04-131">Hola te mostramos una plantilla en formato de archivo de hello json:</span><span class="sxs-lookup"><span data-stu-id="1bc04-131">hello following is a template in hello json file format:</span></span>

```
{ 
   "ConnectionFields": [
   {
      "IsEncrypted":  false,
      "IsOptional":  false,
      "Name":  "ComputerName",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  false,
      "IsOptional":  true,
      "Name":  "Username",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  true,
      "IsOptional":  false,
      "Name":  "Password",
   "TypeName":  "System.String"
   }],
   "ConnectionTypeName":  "DataProtectionManager",
   "IntegrationModuleName":  "DataProtectionManager"
}
```

<span data-ttu-id="1bc04-132">Si ha implementado Service Management Automation y crear paquetes de módulos de integración para los runbooks de automatización, este debe tener un aspecto muy familiar tooyou.</span><span class="sxs-lookup"><span data-stu-id="1bc04-132">If you have deployed Service Management Automation and created Integration Modules packages for your automation runbooks, this should look very familiar tooyou.</span></span> 

## <a name="authoring-best-practices"></a><span data-ttu-id="1bc04-133">Procedimientos recomendados sobre la creación de los módulos</span><span class="sxs-lookup"><span data-stu-id="1bc04-133">Authoring Best Practices</span></span>
<span data-ttu-id="1bc04-134">Aunque módulos de integración son básicamente los módulos de PowerShell, hay varias cosas que se recomienda que considere la posibilidad de mientras se crea un módulo de PowerShell, toomake lo más utilizable en automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="1bc04-134">Even though Integration Modules are essentially PowerShell modules, there’s still a number of things we recommend you consider while authoring a PowerShell module, toomake it most usable in Azure Automation.</span></span> <span data-ttu-id="1bc04-135">Algunos de ellos son específicos de automatización de Azure y algunas de ellas son útil toomake solo los módulos funcionan bien en el flujo de trabajo de PowerShell, independientemente de si usas la automatización.</span><span class="sxs-lookup"><span data-stu-id="1bc04-135">Some of these are Azure Automation specific, and some of them are useful just toomake your modules work well in PowerShell Workflow, regardless of whether or not you’re using Automation.</span></span> 

1. <span data-ttu-id="1bc04-136">Incluir una sinopsis, descripción y ayudar a los URI para todos los cmdlets de módulo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bc04-136">Include a synopsis, description, and help URI for every cmdlet in hello module.</span></span> <span data-ttu-id="1bc04-137">En PowerShell, puede definir cierta información de ayuda para cmdlets tooallow Hola usuario tooreceive ayuda acerca de cómo utilizarlas con hello **Get-Help** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1bc04-137">In PowerShell, you can define certain help information for cmdlets tooallow hello user tooreceive help on using them with hello **Get-Help** cmdlet.</span></span> <span data-ttu-id="1bc04-138">Por ejemplo, a continuación le mostramos cómo puede definir una sinopsis y un identificador URI de ayuda para un módulo de PowerShell escrito en un archivo .psm1.</span><span class="sxs-lookup"><span data-stu-id="1bc04-138">For example, here’s how you can define a synopsis and help URI for a PowerShell module written in a .psm1 file.</span></span><br>  
   
    ```
    <#
        .SYNOPSIS
         Gets all outgoing phone numbers for this Twilio account 
    #>
    function Get-TwilioPhoneNumbers {
    [CmdletBinding(DefaultParameterSetName='SpecifyConnectionFields', `
    HelpUri='http://www.twilio.com/docs/api/rest/outgoing-caller-ids')]
    param(
       [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [string]
       $AccountSid,
   
       [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [string]
       $AuthToken,
   
       [Parameter(ParameterSetName='UseConnectionObject', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [Hashtable]
       $Connection
    )
   
    $cred = CreateTwilioCredential -Connection $Connection -AccountSid $AccountSid -AuthToken $AuthToken
   
    $uri = "$TWILIO_BASE_URL/Accounts/" + $cred.UserName + "/IncomingPhoneNumbers"
   
    $response = Invoke-RestMethod -Method Get -Uri $uri -Credential $cred
   
    $response.TwilioResponse.IncomingPhoneNumbers.IncomingPhoneNumber
    }
    ```
   <br> <span data-ttu-id="1bc04-139">Proporcionar esta información, no solo se mostrarán esta ayuda sobre el uso de hello **Get-Help** Hola de cmdlet en consola de PowerShell, también va a exponer esta funcionalidad ayuda en automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="1bc04-139">Providing this info will not only show this help using hello **Get-Help** cmdlet in hello PowerShell console, it will also expose this help functionality within Azure Automation.</span></span>  <span data-ttu-id="1bc04-140">Por ejemplo, al insertar actividades durante la creación de runbooks.</span><span class="sxs-lookup"><span data-stu-id="1bc04-140">For example, when inserting activities during runbook authoring.</span></span> <span data-ttu-id="1bc04-141">Haga clic en "Ver ayuda detallada" se ayuda URI de hello abierto en otra ficha del programa Hola a web explorador está usando tooaccess automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="1bc04-141">Clicking “View detailed help” will open hello help URI in another tab of hello web browser you’re using tooaccess Azure Automation.</span></span><br><span data-ttu-id="1bc04-142">![Ayuda para los módulos de integración](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span><span class="sxs-lookup"><span data-stu-id="1bc04-142">![Integration Module Help](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span></span>
2. <span data-ttu-id="1bc04-143">Si el módulo de Hola se ejecuta en un sistema remoto,</span><span class="sxs-lookup"><span data-stu-id="1bc04-143">If hello module runs against a remote system,</span></span>

    <span data-ttu-id="1bc04-144">a.</span><span class="sxs-lookup"><span data-stu-id="1bc04-144">a.</span></span> <span data-ttu-id="1bc04-145">Debe contener un archivo de metadatos del módulo de integración que define Hola información necesaria tooconnect toothat sistema remoto, lo que significa que el tipo de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bc04-145">It should contain an Integration Module metadata file that defines hello information needed tooconnect toothat remote system, meaning hello connection type.</span></span>  
    <span data-ttu-id="1bc04-146">b.</span><span class="sxs-lookup"><span data-stu-id="1bc04-146">b.</span></span> <span data-ttu-id="1bc04-147">Cada cmdlet en el módulo de hello debe ser capaz de tootake en un objeto de conexión (una instancia de ese tipo de conexión) como un parámetro.</span><span class="sxs-lookup"><span data-stu-id="1bc04-147">Each cmdlet in hello module should be able tootake in a connection object (an instance of that connection type) as a parameter.</span></span>  

    <span data-ttu-id="1bc04-148">Cmdlets de módulo de Hola se convierten en toouse más fácil en automatización de Azure si permite pasar un objeto con campos de hello del tipo de conexión de Hola como un cmdlet de toohello de parámetro.</span><span class="sxs-lookup"><span data-stu-id="1bc04-148">Cmdlets in hello module become easier toouse in Azure Automation if you allow passing an object with hello fields of hello connection type as a parameter toohello cmdlet.</span></span> <span data-ttu-id="1bc04-149">Esta forma, los usuarios no tienen parámetros de toomap de los parámetros correspondientes del cmdlet de hello connection asset toohello cada vez que llame a un cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1bc04-149">This way users don’t have toomap parameters of hello connection asset toohello cmdlet's corresponding parameters each time they call a cmdlet.</span></span> <span data-ttu-id="1bc04-150">Tomando como ejemplo de Hola runbook anterior, utiliza un activo de conexión de Twilio denominado CorpTwilio tooaccess Twilio y devolver todos los números de teléfono de hello en la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="1bc04-150">Based on hello runbook example above, it uses a Twilio connection asset called CorpTwilio tooaccess Twilio and return all hello phone numbers in hello account.</span></span>  <span data-ttu-id="1bc04-151">¿Tenga en cuenta cómo se trata de asignar campos de Hola Hola toohello de parámetros de conexión del cmdlet Hola?</span><span class="sxs-lookup"><span data-stu-id="1bc04-151">Notice how it is mapping hello fields of hello connection toohello parameters of hello cmdlet?</span></span><br>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers 
        -AccountSid $CorpTwilio.AccountSid  
        -AuthToken $CorptTwilio.AuthToken
    }
    ```
  
    <span data-ttu-id="1bc04-152">Una manera más fácil y mejor tooapproach directamente esto está pasando Hola conexión objeto toohello cmdlet-</span><span class="sxs-lookup"><span data-stu-id="1bc04-152">An easier and better way tooapproach this is directly passing hello connection object toohello cmdlet -</span></span>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers -Connection $CorpTwilio
    }
    ```
   
    <span data-ttu-id="1bc04-153">Puede habilitar el comportamiento parecido a esto para sus cmdlets, permitiéndoles tooaccept un objeto de conexión directamente como un parámetro, en lugar de simplemente los campos de conexión para los parámetros.</span><span class="sxs-lookup"><span data-stu-id="1bc04-153">You can enable behavior like this for your cmdlets by allowing them tooaccept a connection object directly as a parameter, instead of just connection fields for parameters.</span></span> <span data-ttu-id="1bc04-154">Por lo general debe tener un parámetro establecido para cada uno, por lo que un usuario no usar la automatización de Azure puede llamar a los cmdlets sin generar un tooact de tabla hash como objeto de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bc04-154">Usually you’ll want a parameter set for each, so that a user not using Azure Automation can call your cmdlets without constructing a hashtable tooact as hello connection object.</span></span> <span data-ttu-id="1bc04-155">Conjunto de parámetros **SpecifyConnectionFields** a continuación se muestra toopass usa propiedades de campo de conexión de hello uno por uno.</span><span class="sxs-lookup"><span data-stu-id="1bc04-155">Parameter set **SpecifyConnectionFields** below is used toopass hello connection field properties one by one.</span></span> <span data-ttu-id="1bc04-156">**UseConnectionObject** permite pasar Hola directamente a través de la conexión.</span><span class="sxs-lookup"><span data-stu-id="1bc04-156">**UseConnectionObject** lets you pass hello connection straight through.</span></span> <span data-ttu-id="1bc04-157">Como puede ver, Hola cmdlet envío TwilioSMS Hola [Twilio PowerShell módulo](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) permite pasar cualquier modo:</span><span class="sxs-lookup"><span data-stu-id="1bc04-157">As you can see, hello Send-TwilioSMS cmdlet in hello [Twilio PowerShell module](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) allows passing either way:</span></span> 
   
    ```
    function Send-TwilioSMS {
      [CmdletBinding(DefaultParameterSetName='SpecifyConnectionFields', `
      HelpUri='http://www.twilio.com/docs/api/rest/sending-sms')]
      param(
         [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [string]
         $AccountSid,
   
         [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [string]
         $AuthToken,
   
         [Parameter(ParameterSetName='UseConnectionObject', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [Hashtable]
         $Connection
   
       )
    }
    ```
   <br>
3. <span data-ttu-id="1bc04-158">Defina el tipo de salida de todos los cmdlets en el módulo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bc04-158">Define output type for all cmdlets in hello module.</span></span> <span data-ttu-id="1bc04-159">Al definir un tipo de salida de un cmdlet permite IntelliSense en tiempo de diseño toohelp determinar Hola enviar propiedades del cmdlet de hello, para su uso durante la creación.</span><span class="sxs-lookup"><span data-stu-id="1bc04-159">Defining an output type for a cmdlet allows design-time IntelliSense toohelp you determine hello output properties of hello cmdlet, for use during authoring.</span></span> <span data-ttu-id="1bc04-160">Es especialmente útil durante la automatización gráfica creación de runbooks, donde conocimiento de tiempo de diseño es la experiencia de usuario sencilla tooan clave con el módulo.</span><span class="sxs-lookup"><span data-stu-id="1bc04-160">It is especially helpful during Automation runbook graphical authoring, where design time knowledge is key tooan easy user experience with your module.</span></span><br><br> <span data-ttu-id="1bc04-161">![Tipo de salida de runbooks gráficos](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span><span class="sxs-lookup"><span data-stu-id="1bc04-161">![Graphical Runbook Output Type](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span></span><br> <span data-ttu-id="1bc04-162">Esto es similar toohello "con antelación de tipo" funcionalidad de un cmdlet de salida de la en PowerShell ISE sin necesidad de toorun lo.</span><span class="sxs-lookup"><span data-stu-id="1bc04-162">This is similar toohello "type ahead" functionality of a cmdlet's output in PowerShell ISE without having toorun it.</span></span><br><br> <span data-ttu-id="1bc04-163">![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span><span class="sxs-lookup"><span data-stu-id="1bc04-163">![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span></span><br>
4. <span data-ttu-id="1bc04-164">Cmdlets de módulo de hello no debería tardar tipos de objeto complejo para los parámetros.</span><span class="sxs-lookup"><span data-stu-id="1bc04-164">Cmdlets in hello module should not take complex object types for parameters.</span></span> <span data-ttu-id="1bc04-165">El flujo de trabajo de PowerShell se diferencia del propio PowerShell en que almacena tipos complejos con formato deserializado.</span><span class="sxs-lookup"><span data-stu-id="1bc04-165">PowerShell Workflow is different from PowerShell in that it stores complex types in deserialized form.</span></span> <span data-ttu-id="1bc04-166">Permanecerán tipos primitivos como tipos primitivos, pero los tipos complejos son versiones de tootheir convertido deserializada, que son esencialmente los contenedores de propiedades.</span><span class="sxs-lookup"><span data-stu-id="1bc04-166">Primitive types will stay as primitives, but complex types are converted tootheir deserialized versions, which are essentially property bags.</span></span> <span data-ttu-id="1bc04-167">Por ejemplo, si utiliza hello **Get-Process** cmdlet en un runbook (o un flujo de trabajo de PowerShell para este propósito), devuelven un objeto de tipo [Deserialized.System.Diagnostic.Process], no Hola [esperado Tipo de System.Diagnostic.Process].</span><span class="sxs-lookup"><span data-stu-id="1bc04-167">For example, if you used hello **Get-Process** cmdlet in a runbook (or a PowerShell Workflow for that matter), it would return an object of type [Deserialized.System.Diagnostic.Process], not hello expected [System.Diagnostic.Process] type.</span></span> <span data-ttu-id="1bc04-168">Este tipo tiene todas Hola mismas propiedades como Hola no deserializar el tipo, pero ninguno de los métodos de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bc04-168">This type has all hello same properties as hello non-deserialized type, but none of hello methods.</span></span> <span data-ttu-id="1bc04-169">Si intentas toopass este valor como un cmdlet de tooa parámetro, donde hello cmdlet espera un valor de [System.Diagnostic.Process] para este parámetro, recibirá Hola siguiente error: *no se puede procesar la transformación de argumento en el parámetro 'process' . Error: "no se puede convertir el valor de"System.Diagnostics.Process (CcmExec)"¡hello de tipo"Deserialized.System.Diagnostics.Process"tootype"System.Diagnostics.Process".*</span><span class="sxs-lookup"><span data-stu-id="1bc04-169">And if you try toopass this value as a parameter tooa cmdlet, where hello cmdlet expects a [System.Diagnostic.Process] value for this parameter, you’ll receive hello following error: *Cannot process argument transformation on parameter 'process'. Error: "Cannot convert hello "System.Diagnostics.Process (CcmExec)" value of type  "Deserialized.System.Diagnostics.Process" tootype "System.Diagnostics.Process".*</span></span>   <span data-ttu-id="1bc04-170">Esto es porque no hay que una discordancia de tipos entre Hola espera hello dado tipo [Deserialized.System.Diagnostic.Process] y [System.Diagnostic.Process] tipo.</span><span class="sxs-lookup"><span data-stu-id="1bc04-170">This is because there is a type mismatch between hello expected [System.Diagnostic.Process] type and hello given [Deserialized.System.Diagnostic.Process] type.</span></span> <span data-ttu-id="1bc04-171">forma de Hello alternativa a este problema es tooensure Hola cmdlets del módulo no tienen tipos complejos de parámetros.</span><span class="sxs-lookup"><span data-stu-id="1bc04-171">hello way around this issue is tooensure hello cmdlets of your module do not take complex types for parameters.</span></span> <span data-ttu-id="1bc04-172">Aquí es toodo de manera incorrecta de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bc04-172">Here is hello wrong way toodo it.</span></span>
   
    ```
    function Get-ProcessDescription {
      param (
            [System.Diagnostic.Process] $process
      )
      $process.Description
    }
    ``` 
    <br>
    <span data-ttu-id="1bc04-173">A continuación se Hola derecho a propósito, en un tipo primitivo que puede utilizarse internamente mediante el cmdlet hello toograb Hola objeto complejo y usarlo.</span><span class="sxs-lookup"><span data-stu-id="1bc04-173">And here is hello right way, taking in a primitive that can be used internally by hello cmdlet toograb hello complex object and use it.</span></span> <span data-ttu-id="1bc04-174">Puesto que los cmdlets se ejecutan en el contexto de Hola de PowerShell, no PowerShell flujos de trabajo dentro de cmdlet de hello $process se convierte en tipo de [System.Diagnostic.Process] correcto de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bc04-174">Since cmdlets execute in hello context of PowerShell, not PowerShell Workflow, inside hello cmdlet $process becomes hello correct [System.Diagnostic.Process] type.</span></span>  
   
    ```
    function Get-ProcessDescription {
      param (
            [String] $processName
      )
      $process = Get-Process -Name $processName
   
      $process.Description
    }
    ```
   <br>
   <span data-ttu-id="1bc04-175">Activos de conexión en los runbooks son tablas hash, que son un tipo complejo, y aún estas tablas hash parece toobe toobe puede pasado a cmdlets para sus: parámetro de conexión perfectamente, con ninguna excepción de conversión.</span><span class="sxs-lookup"><span data-stu-id="1bc04-175">Connection assets in runbooks are hashtables, which are a complex type, and yet these hashtables seem toobe able toobe passed into cmdlets for their –Connection parameter perfectly, with no cast exception.</span></span> <span data-ttu-id="1bc04-176">Técnicamente, algunos tipos de PowerShell son toocast capaz de correctamente desde su forma de tootheir deserializada forma serializada y por lo tanto, pueden pasarse a cmdlets de para los parámetros que admite elección de tipo no deserializa de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bc04-176">Technically, some PowerShell types are able toocast properly from their serialized form tootheir deserialized form, and hence can be passed into cmdlets for parameters accepting hello non-deserialized type.</span></span> <span data-ttu-id="1bc04-177">Las tablas hash son uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="1bc04-177">Hashtable is one of these.</span></span> <span data-ttu-id="1bc04-178">Es posible que toobe de tipos definidos del autor de un módulo implementada de modo que puede deserializar correctamente así, pero hay algunos tooconsider ventajas e inconvenientes.</span><span class="sxs-lookup"><span data-stu-id="1bc04-178">It’s possible for a module author’s defined types toobe implemented in a way that they can correctly deserialize as well, but there are some trade-offs tooconsider.</span></span> <span data-ttu-id="1bc04-179">Hola tipo necesidades toohave un constructor predeterminado, tiene todas sus propiedades públicas y tener un PSTypeConverter.</span><span class="sxs-lookup"><span data-stu-id="1bc04-179">hello type needs toohave a default constructor, have all of its properties public, and have a PSTypeConverter.</span></span> <span data-ttu-id="1bc04-180">Sin embargo, para tipos ya definidos por el autor del módulo de hello no posee, hay no demasiado "corregirlos", por lo tanto, Hola tipos complejos de recomendación tooavoid para parámetros todos juntos.</span><span class="sxs-lookup"><span data-stu-id="1bc04-180">However, for already-defined types that hello module author does not own, there is no way too“fix” them, hence hello recommendation tooavoid complex types for parameters all together.</span></span> <span data-ttu-id="1bc04-181">Creación de runbooks Sugerencia: si por alguna razón su cmdlets necesita el parámetro de tipo de tootake complejo o que usa de otra persona módulo que requiere un parámetro de tipo complejo, la solución de hello en los runbooks de flujo de trabajo de PowerShell y flujos de trabajo de PowerShell local PowerShell, es toowrap Hola cmdlet que genera el tipo complejo de Hola y Hola cmdlet que consume el tipo complejo de Hola Hola misma actividad de InlineScript.</span><span class="sxs-lookup"><span data-stu-id="1bc04-181">Runbook Authoring tip: If for some reason your cmdlets need tootake a complex type parameter, or you are using someone else’s module that requires a complex type parameter, hello workaround in PowerShell Workflow runbooks and PowerShell Workflows in local PowerShell, is toowrap hello cmdlet that generates hello complex type and hello cmdlet that consumes hello complex type in hello same InlineScript activity.</span></span> <span data-ttu-id="1bc04-182">Como InlineScript ejecuta su contenido como PowerShell en lugar de flujo de trabajo de PowerShell, cmdlet Hola generar tipo complejo de hello generaría ese tipo correcto, no Hola deserializa el tipo complejo.</span><span class="sxs-lookup"><span data-stu-id="1bc04-182">Since InlineScript executes its contents as PowerShell rather than PowerShell Workflow, hello cmdlet generating hello complex type would produce that correct type, not hello deserialized complex type.</span></span>
5. <span data-ttu-id="1bc04-183">Asegúrese de todos los cmdlets en el módulo de hello sin estado.</span><span class="sxs-lookup"><span data-stu-id="1bc04-183">Make all cmdlets in hello module stateless.</span></span> <span data-ttu-id="1bc04-184">Flujo de trabajo de PowerShell se ejecuta cada cmdlet denominado en el flujo de trabajo de hello en una sesión diferente.</span><span class="sxs-lookup"><span data-stu-id="1bc04-184">PowerShell Workflow runs every cmdlet called in hello workflow in a different session.</span></span> <span data-ttu-id="1bc04-185">Esto significa que los cmdlets que dependen de estado de sesión creado o modificado por otros cmdlets Hola mismo módulo no funcionará en los runbooks de flujo de trabajo de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1bc04-185">This means any cmdlets that depend on session state created / modified by other cmdlets in hello same module will not work in PowerShell Workflow runbooks.</span></span>  <span data-ttu-id="1bc04-186">Este es un ejemplo de lo que no toodo.</span><span class="sxs-lookup"><span data-stu-id="1bc04-186">Here is an example of what not toodo.</span></span>
   
    ```
    $globalNum = 0
    function Set-GlobalNum {
       param(
           [int] $num
       )
   
       $globalNum = $num
    }
    function Get-GlobalNumTimesTwo {
       $output = $globalNum * 2
   
       $output
    }
    ```
   <br>
6. <span data-ttu-id="1bc04-187">módulo de Hello debe estar totalmente contenida en un paquete capaz de Xcopy.</span><span class="sxs-lookup"><span data-stu-id="1bc04-187">hello module should be fully contained in an Xcopy-able package.</span></span> <span data-ttu-id="1bc04-188">Dado que los módulos de automatización de Azure son espacios aislados de automatización distribuida toohello cuando runbooks necesario tooexecute, deben toowork independientemente de que se ejecutan en el host de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bc04-188">Because Azure Automation modules are distributed toohello Automation sandboxes when runbooks need tooexecute, they need toowork independently of hello host they are running on.</span></span> <span data-ttu-id="1bc04-189">Esto significa que debe ser capaz de tooZip paquete de módulo de hello, muévalo tooany otro host con Hola versión de PowerShell igual o más recientes, y para que funcione con normalidad cuando se importan en el entorno de PowerShell de ese host.</span><span class="sxs-lookup"><span data-stu-id="1bc04-189">What this means is that you should be able tooZip up hello module package, move it tooany other host with hello same or newer PowerShell version, and have it function as normal when imported into that host’s PowerShell environment.</span></span> <span data-ttu-id="1bc04-190">En orden para que toohappen, módulo de hello no debe depender de los archivos fuera de la carpeta de módulo de hello (carpeta de Hola que obtiene comprimirán al importar en la automatización de Azure), o en cualquier configuración de registro único en un host, como las que se establecen por Hola la instalación de un producto.</span><span class="sxs-lookup"><span data-stu-id="1bc04-190">In order for that toohappen, hello module should not depend on any files outside hello module folder (hello folder that gets zipped up when importing into Azure Automation), or on any unique registry settings on a host, such as those set by hello install of a product.</span></span> <span data-ttu-id="1bc04-191">Si no se respeta esta práctica recomendada, módulo de hello no podrá utilizarse en automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="1bc04-191">If this best practice is not followed, hello module will not be usable in Azure Automation.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="1bc04-192">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1bc04-192">Next steps</span></span>

* <span data-ttu-id="1bc04-193">tooget a trabajar con runbooks de flujo de trabajo de PowerShell, consulte [mi primer runbook de flujo de trabajo de PowerShell](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="1bc04-193">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="1bc04-194">toolearn más información acerca de la creación de módulos de PowerShell, consulte [escribir un módulo de Windows PowerShell](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="1bc04-194">toolearn more about creating PowerShell Modules, see [Writing a Windows PowerShell Module](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span></span>

