---
title: "aaaCreate una canalización de CI/CD en Azure con Team Services | Documentos de Microsoft"
description: "Obtenga información acerca de cómo de canalización toocreate un Visual Studio Team Services para la integración continua y entrega que implementa un tooIIS de aplicación web en una máquina virtual de Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: b758a124c4742854dd3b543f747fd8700f954414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-continuous-integration-pipeline-with-visual-studio-team-services-and-iis"></a><span data-ttu-id="2df46-103">Creación de una canalización de integración continua con Visual Studio Team Services e IIS</span><span class="sxs-lookup"><span data-stu-id="2df46-103">Create a continuous integration pipeline with Visual Studio Team Services and IIS</span></span>
<span data-ttu-id="2df46-104">tooautomate Hola compilación, prueba y fases de implementación del desarrollo de aplicaciones, puede usar una integración continua y la canalización de implementación (CI/CD).</span><span class="sxs-lookup"><span data-stu-id="2df46-104">tooautomate hello build, test, and deployment phases of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="2df46-105">En este tutorial se creará una canalización CI/CD utilizando Visual Studio Team Services y una máquina virtual Windows en Azure que ejecuta IIS.</span><span class="sxs-lookup"><span data-stu-id="2df46-105">In this tutorial, you create a CI/CD pipeline using Visual Studio Team Services and a Windows virtual machine (VM) in Azure that runs IIS.</span></span> <span data-ttu-id="2df46-106">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="2df46-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2df46-107">Publicar un proyecto de Team Services de tooa de aplicación web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="2df46-107">Publish an ASP.NET web application tooa Team Services project</span></span>
> * <span data-ttu-id="2df46-108">Crear una definición de compilación que se desencadena mediante confirmaciones de código</span><span class="sxs-lookup"><span data-stu-id="2df46-108">Create a build definition that is triggered by code commits</span></span>
> * <span data-ttu-id="2df46-109">Instalar y configurar IIS en una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="2df46-109">Install and configure IIS on a virtual machine in Azure</span></span>
> * <span data-ttu-id="2df46-110">Agregar grupo de implementación de tooa de instancia IIS de hello en Team Services</span><span class="sxs-lookup"><span data-stu-id="2df46-110">Add hello IIS instance tooa deployment group in Team Services</span></span>
> * <span data-ttu-id="2df46-111">Crear un nuevo web de versión definición toopublish implementar paquetes tooIIS</span><span class="sxs-lookup"><span data-stu-id="2df46-111">Create a release definition toopublish new web deploy packages tooIIS</span></span>
> * <span data-ttu-id="2df46-112">Probar Hola CI/CD canalización</span><span class="sxs-lookup"><span data-stu-id="2df46-112">Test hello CI/CD pipeline</span></span>

<span data-ttu-id="2df46-113">Este tutorial requiere hello Azure PowerShell versión 3.6 o posterior del módulo.</span><span class="sxs-lookup"><span data-stu-id="2df46-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="2df46-114">Ejecutar `Get-Module -ListAvailable AzureRM` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="2df46-114">Run `Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="2df46-115">Si necesita tooupgrade, consulte [módulo instalar Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="2df46-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="create-project-in-team-services"></a><span data-ttu-id="2df46-116">Crear el proyecto en Team Services</span><span class="sxs-lookup"><span data-stu-id="2df46-116">Create project in Team Services</span></span>
<span data-ttu-id="2df46-117">Visual Studio Team Services permite una colaboración y desarrollo sencillos sin mantener una solución de administración de código local.</span><span class="sxs-lookup"><span data-stu-id="2df46-117">Visual Studio Team Services allows for easy collaboration and development without maintaining an on-premises code management solution.</span></span> <span data-ttu-id="2df46-118">Team Services proporciona pruebas de código en la nube, compilación y visión de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2df46-118">Team Services provides cloud code testing, build, and application insights.</span></span> <span data-ttu-id="2df46-119">Puede elegir el repositorio de control de versiones y el IDE que mejor se adapten a su desarrollo de código.</span><span class="sxs-lookup"><span data-stu-id="2df46-119">You can choose a version control repo and IDE that best fits your code development.</span></span> <span data-ttu-id="2df46-120">Para este tutorial, puede usar una cuenta gratuita toocreate una aplicación web ASP.NET básica y la canalización de CI/CD.</span><span class="sxs-lookup"><span data-stu-id="2df46-120">For this tutorial, you can use a free account toocreate a basic ASP.NET web app and CI/CD pipeline.</span></span> <span data-ttu-id="2df46-121">Si no dispone de una cuenta de Team Services, [cree una](http://go.microsoft.com/fwlink/?LinkId=307137).</span><span class="sxs-lookup"><span data-stu-id="2df46-121">If you do not already have a Team Services account, [create one](http://go.microsoft.com/fwlink/?LinkId=307137).</span></span>

<span data-ttu-id="2df46-122">proceso de confirmación de código de hello toomanage, definiciones, de compilación y las definiciones de la versión, crear un proyecto en Team Services como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="2df46-122">toomanage hello code commit process, build definitions, and release definitions, create a project in Team Services as follows:</span></span>

1. <span data-ttu-id="2df46-123">Abra el panel de Team Services en un explorador web y elija **Nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="2df46-123">Open your Team Services dashboard in a web browser and choose **New project**.</span></span>
2. <span data-ttu-id="2df46-124">Escriba *myWebApp* para hello **nombre del proyecto**.</span><span class="sxs-lookup"><span data-stu-id="2df46-124">Enter *myWebApp* for hello **Project name**.</span></span> <span data-ttu-id="2df46-125">Dejar todos los demás toouse de valores predeterminado *Git* control de versiones y *Agile* proceso de elemento de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2df46-125">Leave all other default values toouse *Git* version control and *Agile* work item process.</span></span>
3. <span data-ttu-id="2df46-126">Elija la opción de hello demasiado**compartir con** *los miembros del equipo*, a continuación, seleccione **crear**.</span><span class="sxs-lookup"><span data-stu-id="2df46-126">Choose hello option too**Share with** *Team Members*, then select **Create**.</span></span>
5. <span data-ttu-id="2df46-127">Una vez creado el proyecto, elija la opción de hello demasiado**inicializar con un archivo Léame o gitignore**, a continuación, **inicializar**.</span><span class="sxs-lookup"><span data-stu-id="2df46-127">Once your project has been created, choose hello option too**Initialize with a README or gitignore**, then **Initialize**.</span></span>
6. <span data-ttu-id="2df46-128">En el proyecto nuevo, elija **paneles** a través de la parte superior de hello, a continuación, seleccione **abierta en Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="2df46-128">Inside your new project, choose **Dashboards** across hello top, then select **Open in Visual Studio**.</span></span>


## <a name="create-aspnet-web-application"></a><span data-ttu-id="2df46-129">Creación de una aplicación web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="2df46-129">Create ASP.NET web application</span></span>
<span data-ttu-id="2df46-130">En el paso anterior de hello, creó un proyecto en Team Services.</span><span class="sxs-lookup"><span data-stu-id="2df46-130">In hello previous step, you created a project in Team Services.</span></span> <span data-ttu-id="2df46-131">paso final de Hello abre el proyecto nuevo en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2df46-131">hello final step opens your new project in Visual Studio.</span></span> <span data-ttu-id="2df46-132">Administrar las confirmaciones de código de hello **Team Explorer** ventana.</span><span class="sxs-lookup"><span data-stu-id="2df46-132">You manage your code commits in hello **Team Explorer** window.</span></span> <span data-ttu-id="2df46-133">Cree una copia local del nuevo proyecto y, a continuación, cree una aplicación web ASP.NET a partir de una plantilla, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="2df46-133">Create a local copy of your new project, then create an ASP.NET web application from a template as follows:</span></span>

1. <span data-ttu-id="2df46-134">Seleccione **clon** toocreate un repositorio de git local de su proyecto de Team Services.</span><span class="sxs-lookup"><span data-stu-id="2df46-134">Select **Clone** toocreate a local git repo of your Team Services project.</span></span>
    
    ![Clonación del repositorio del proyecto de Team Services](media/tutorial-vsts-iis-cicd/clone_repo.png)

2. <span data-ttu-id="2df46-136">En **Soluciones**, seleccione **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="2df46-136">Under **Solutions**, select **New**.</span></span>

    ![Creación de la solución de aplicación web](media/tutorial-vsts-iis-cicd/new_solution.png)

3. <span data-ttu-id="2df46-138">Seleccione **Web** plantillas y, a continuación, elija hello **aplicación Web ASP.NET** plantilla.</span><span class="sxs-lookup"><span data-stu-id="2df46-138">Select **Web** templates, and then choose hello **ASP.NET Web Application** template.</span></span>
    1. <span data-ttu-id="2df46-139">Escriba un nombre para la aplicación, como *myWebApp*y desactive la casilla de Hola para **crear directorio para la solución**.</span><span class="sxs-lookup"><span data-stu-id="2df46-139">Enter a name for your application, such as *myWebApp*, and uncheck hello box for **Create directory for solution**.</span></span>
    2. <span data-ttu-id="2df46-140">Si está disponible la opción de hello, desactive la casilla cuadro Hola demasiado**tooproject agregar Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="2df46-140">If hello option is available, uncheck hello box too**Add Application Insights tooproject**.</span></span> <span data-ttu-id="2df46-141">Visión de la aplicación requiere tooauthorize su aplicación web con Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="2df46-141">Application Insights requires you tooauthorize your web application with Azure Application Insights.</span></span> <span data-ttu-id="2df46-142">tookeep que simple en este tutorial, omita este proceso.</span><span class="sxs-lookup"><span data-stu-id="2df46-142">tookeep it simple in this tutorial, skip this process.</span></span>
    3. <span data-ttu-id="2df46-143">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2df46-143">Select **OK**.</span></span>
4. <span data-ttu-id="2df46-144">Elija **MVC** de lista de plantillas de Hola.</span><span class="sxs-lookup"><span data-stu-id="2df46-144">Choose **MVC** from hello template list.</span></span>
    1. <span data-ttu-id="2df46-145">Seleccione **Cambiar autenticación**, elija **Sin autenticación** y, a continuación, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2df46-145">Select **Change Authentication**, choose **No Authentication**, then select **OK**.</span></span>
    2. <span data-ttu-id="2df46-146">Seleccione **Aceptar** toocreate la solución.</span><span class="sxs-lookup"><span data-stu-id="2df46-146">Select **OK** toocreate your solution.</span></span>
5. <span data-ttu-id="2df46-147">Hola **Team Explorer** ventana, elija **cambios**.</span><span class="sxs-lookup"><span data-stu-id="2df46-147">In hello **Team Explorer** window, choose **Changes**.</span></span>

    ![Confirmar el repositorio de git de servicios de tooTeam cambios locales](media/tutorial-vsts-iis-cicd/commit_changes.png)

6. <span data-ttu-id="2df46-149">En el cuadro de texto de confirmación de hello, escriba un mensaje como *confirmación inicial*.</span><span class="sxs-lookup"><span data-stu-id="2df46-149">In hello commit text box, enter a message such as *Initial commit*.</span></span> <span data-ttu-id="2df46-150">Elija **confirmar todos y sincronización** desde el menú desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="2df46-150">Choose **Commit All and Sync** from hello drop-down menu.</span></span>


## <a name="create-build-definition"></a><span data-ttu-id="2df46-151">Creación de la definición de compilación</span><span class="sxs-lookup"><span data-stu-id="2df46-151">Create build definition</span></span>
<span data-ttu-id="2df46-152">En Team Services, use un toooutline de definición de compilación cómo debe crearse la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2df46-152">In Team Services, you use a build definition toooutline how your application should be built.</span></span> <span data-ttu-id="2df46-153">En este tutorial, creamos una definición básica que toma el código fuente, compila la solución de hello, a continuación, crea web implementa paquete podemos usar toorun hello web app en un servidor IIS.</span><span class="sxs-lookup"><span data-stu-id="2df46-153">In this tutorial, we create a basic definition that takes our source code, builds hello solution, then creates web deploy package we can use toorun hello web app on an IIS server.</span></span>

1. <span data-ttu-id="2df46-154">En el proyecto de Team Services, elija **compilar & versión** a través de la parte superior de hello, a continuación, seleccione **genera**.</span><span class="sxs-lookup"><span data-stu-id="2df46-154">In your Team Services project, choose **Build & Release** across hello top, then select **Builds**.</span></span>
3. <span data-ttu-id="2df46-155">Seleccione **+ Nueva definición**.</span><span class="sxs-lookup"><span data-stu-id="2df46-155">Select **+ New definition**.</span></span>
4. <span data-ttu-id="2df46-156">Elija hello **ASP.NET (versión preliminar)** plantilla y seleccione **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="2df46-156">Choose hello **ASP.NET (PREVIEW)** template and select **Apply**.</span></span>
5. <span data-ttu-id="2df46-157">Deje predeterminado de hello todos los valores de la tarea.</span><span class="sxs-lookup"><span data-stu-id="2df46-157">Leave all hello default task values.</span></span> <span data-ttu-id="2df46-158">En **obtener orígenes**, asegúrese de que hello *myWebApp* repositorio y *maestro* bifurcación está seleccionada.</span><span class="sxs-lookup"><span data-stu-id="2df46-158">Under **Get sources**, ensure that hello *myWebApp* repository and *master* branch are selected.</span></span>

    ![Creación de la definición de compilación en el proyecto de Team Services](media/tutorial-vsts-iis-cicd/create_build_definition.png)

6. <span data-ttu-id="2df46-160">En hello **desencadenadores** ficha, mueva el control deslizante de Hola para **habilitar este desencadenador** demasiado*habilitado*.</span><span class="sxs-lookup"><span data-stu-id="2df46-160">On hello **Triggers** tab, move hello slider for **Enable this trigger** too*Enabled*.</span></span>
7. <span data-ttu-id="2df46-161">Guardar definición de compilación de Hola y cola una compilación nueva seleccionando **guardar y poner en cola** , a continuación, **Guardar & cola** nuevo.</span><span class="sxs-lookup"><span data-stu-id="2df46-161">Save hello build definition and queue a new build by selecting **Save & queue** , then **Save & queue** again.</span></span> <span data-ttu-id="2df46-162">Deje los valores predeterminados de Hola y seleccione **cola**.</span><span class="sxs-lookup"><span data-stu-id="2df46-162">Leave hello defaults and select **Queue**.</span></span>

<span data-ttu-id="2df46-163">Inspección compilación Hola programada en un agente hospedado, a continuación, comienza toobuild.</span><span class="sxs-lookup"><span data-stu-id="2df46-163">Watch as hello build is scheduled on a hosted agent, then begins toobuild.</span></span> <span data-ttu-id="2df46-164">Hola de salida es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2df46-164">hello output is similar toohello following example:</span></span>

![Compilación correcta del proyecto de Team Services](media/tutorial-vsts-iis-cicd/successful_build.png)


## <a name="create-virtual-machine"></a><span data-ttu-id="2df46-166">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="2df46-166">Create virtual machine</span></span>
<span data-ttu-id="2df46-167">tooprovide un toorun plataforma la aplicación web ASP.NET, necesita una máquina virtual de Windows que se ejecuta IIS.</span><span class="sxs-lookup"><span data-stu-id="2df46-167">tooprovide a platform toorun your ASP.NET web app, you need a Windows virtual machine that runs IIS.</span></span> <span data-ttu-id="2df46-168">Team Services utiliza un toointeract de agente con la instancia de IIS de hello como Confirmar código y se activan compilaciones.</span><span class="sxs-lookup"><span data-stu-id="2df46-168">Team Services uses an agent toointeract with hello IIS instance as you commit code and builds are triggered.</span></span>

<span data-ttu-id="2df46-169">Cree una máquina virtual Windows Server 2016 mediante [este script de ejemplo](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2df46-169">Create a Windows Server 2016 VM using [this script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json).</span></span> <span data-ttu-id="2df46-170">Se tarda unos minutos para toorun de script de Hola y crear hello VM.</span><span class="sxs-lookup"><span data-stu-id="2df46-170">It takes a few minutes for hello script toorun and create hello VM.</span></span> <span data-ttu-id="2df46-171">Una vez que se ha creado la VM de hello, abrir el puerto 80 para el tráfico web con [AzureRmNetworkSecurityRuleConfig agregar](/powershell/module/azurerm.resources/new-azurermresourcegroup) como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="2df46-171">Once hello VM has been created, open port 80 for web traffic with [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermresourcegroup) as follows:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup `
  -ResourceGroupName $resourceGroup `
  -Name "myNetworkSecurityGroup" | `
Add-AzureRmNetworkSecurityRuleConfig `
  -Name "myNetworkSecurityGroupRuleWeb" `
  -Protocol "Tcp" `
  -Direction "Inbound" `
  -Priority "1001" `
  -SourceAddressPrefix "*" `
  -SourcePortRange "*" `
  -DestinationAddressPrefix "*" `
  -DestinationPortRange "80" `
  -Access "Allow" | `
Set-AzureRmNetworkSecurityGroup
```

<span data-ttu-id="2df46-172">tooconnect tooyour VM, obtener dirección IP pública de hello con [AzureRmPublicIpAddress Get](/powershell/module/azurerm.network/get-azurermpublicipaddress) como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="2df46-172">tooconnect tooyour VM, obtain hello public IP address with [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) as follows:</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName $resourceGroup | Select IpAddress
```

<span data-ttu-id="2df46-173">Crear una máquina virtual de tooyour de sesión de escritorio remoto:</span><span class="sxs-lookup"><span data-stu-id="2df46-173">Create a remote desktop session tooyour VM:</span></span>

```cmd
mstsc /v:<publicIpAddress>
```

<span data-ttu-id="2df46-174">En hello VM, abra un **administrador PowerShell** símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="2df46-174">On hello VM, open an **Administrator PowerShell** command prompt.</span></span> <span data-ttu-id="2df46-175">Instale IIS y las características de .NET necesarias como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="2df46-175">Install IIS and required .NET features as follows:</span></span>

```powershell
Install-WindowsFeature Web-Server,Web-Asp-Net45,NET-Framework-Features
```


## <a name="create-deployment-group"></a><span data-ttu-id="2df46-176">Creación de un grupo de implementación</span><span class="sxs-lookup"><span data-stu-id="2df46-176">Create deployment group</span></span>
<span data-ttu-id="2df46-177">toopush out web Hola implementar paquete toohello al servidor de IIS, defina un grupo de implementación de Team Services.</span><span class="sxs-lookup"><span data-stu-id="2df46-177">toopush out hello web deploy package toohello IIS server, you define a deployment group in Team Services.</span></span> <span data-ttu-id="2df46-178">Este grupo permite toospecify los servidores que son destino de Hola de nuevas compilaciones que confirma tooTeam código servicios y las compilaciones se completan.</span><span class="sxs-lookup"><span data-stu-id="2df46-178">This group allows you toospecify which servers are hello target of new builds as you commit code tooTeam Services and builds are completed.</span></span>

1. <span data-ttu-id="2df46-179">En Team Services, elija **Compilación y versión** y, a continuación, seleccione **Grupos de implementación**.</span><span class="sxs-lookup"><span data-stu-id="2df46-179">In Team Services, choose **Build & Release** and then select **Deployment groups**.</span></span>
2. <span data-ttu-id="2df46-180">Elija **Agregar grupo de implementación**.</span><span class="sxs-lookup"><span data-stu-id="2df46-180">Choose **Add Deployment group**.</span></span>
3. <span data-ttu-id="2df46-181">Escriba un nombre para el grupo de hello, como *myIIS*, a continuación, seleccione **crear**.</span><span class="sxs-lookup"><span data-stu-id="2df46-181">Enter a name for hello group, such as *myIIS*, then select **Create**.</span></span>
4. <span data-ttu-id="2df46-182">Hola **registrar máquinas** sección, asegúrese de *Windows* está seleccionada, la casilla Hola demasiado**usar un token de acceso personal en el script de Hola para la autenticación**.</span><span class="sxs-lookup"><span data-stu-id="2df46-182">In hello **Register machines** section, ensure *Windows* is selected, then check hello box too**Use a personal access token in hello script for authentication**.</span></span>
5. <span data-ttu-id="2df46-183">Seleccione **copiar script tooclipboard**.</span><span class="sxs-lookup"><span data-stu-id="2df46-183">Select **Copy script tooclipboard**.</span></span>


### <a name="add-iis-vm-toohello-deployment-group"></a><span data-ttu-id="2df46-184">Agregar grupo de implementación de IIS VM toohello</span><span class="sxs-lookup"><span data-stu-id="2df46-184">Add IIS VM toohello deployment group</span></span>
<span data-ttu-id="2df46-185">Con grupo de implementación de hello creado, agregue cada grupo de toohello de instancia IIS.</span><span class="sxs-lookup"><span data-stu-id="2df46-185">With hello deployment group created, add each IIS instance toohello group.</span></span> <span data-ttu-id="2df46-186">Servicios de equipo genera un script que se descarga y se configura un agente en implementar la máquina virtual que recibe el nuevo sitio web de Hola paquetes, a continuación, se aplica tooIIS.</span><span class="sxs-lookup"><span data-stu-id="2df46-186">Team Services generates a script that downloads and configures an agent on hello VM that receives new web deploy packages then applies it tooIIS.</span></span>

1. <span data-ttu-id="2df46-187">Nuevo en hello **administrador PowerShell** sesión en la máquina virtual, pegue y ejecute el script de Hola copiado desde Team Services.</span><span class="sxs-lookup"><span data-stu-id="2df46-187">Back in hello **Administrator PowerShell** session on your VM, paste and run hello script copied from Team Services.</span></span>
2. <span data-ttu-id="2df46-188">Cuando se elige etiquetas tooconfigure solicitadas por el agente de hello, *Y* y escriba *web*.</span><span class="sxs-lookup"><span data-stu-id="2df46-188">When prompted tooconfigure tags for hello agent, choose *Y* and enter *web*.</span></span>
3. <span data-ttu-id="2df46-189">Cuando se le solicite para cuenta de usuario de hello, presione *devolver* los valores predeterminados de tooaccept Hola.</span><span class="sxs-lookup"><span data-stu-id="2df46-189">When prompted for hello user account, press *Return* tooaccept hello defaults.</span></span>
4. <span data-ttu-id="2df46-190">Espere Hola script toofinish con un mensaje *vstsagent.account.computername de servicio se inició correctamente*.</span><span class="sxs-lookup"><span data-stu-id="2df46-190">Wait for hello script toofinish with a message *Service vstsagent.account.computername started successfully*.</span></span>
5. <span data-ttu-id="2df46-191">Hola **grupos de implementación** página de hello **de compilación y la versión** menú, abra hello *myIIS* grupo de implementación.</span><span class="sxs-lookup"><span data-stu-id="2df46-191">In hello **Deployment groups** page of hello **Build & Release** menu, open hello *myIIS* deployment group.</span></span> <span data-ttu-id="2df46-192">En hello **máquinas** , compruebe que aparece la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2df46-192">On hello **Machines** tab, verify that your VM is listed.</span></span>

    ![VM agregó correctamente el grupo de implementación de servicios de tooTeam](media/tutorial-vsts-iis-cicd/deployment_group.png)


## <a name="create-release-definition"></a><span data-ttu-id="2df46-194">Creación de la definición de versión</span><span class="sxs-lookup"><span data-stu-id="2df46-194">Create release definition</span></span>
<span data-ttu-id="2df46-195">toopublish las compilaciones, crear una definición de la versión de Team Services.</span><span class="sxs-lookup"><span data-stu-id="2df46-195">toopublish your builds, you create a release definition in Team Services.</span></span> <span data-ttu-id="2df46-196">Esta definición se desencadena automáticamente por una compilación correcta de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2df46-196">This definition is triggered automatically by a successful build of your application.</span></span> <span data-ttu-id="2df46-197">Elija toopush de grupo de implementación de hello web implementa el paquete a y definir la configuración de IIS adecuados de Hola.</span><span class="sxs-lookup"><span data-stu-id="2df46-197">You choose hello deployment group toopush your web deploy package to, and define hello appropriate IIS settings.</span></span>

1. <span data-ttu-id="2df46-198">Elija **Compilación y versión** y, a continuación, seleccione **Compilaciones**.</span><span class="sxs-lookup"><span data-stu-id="2df46-198">Choose **Build & Release**, then select **Builds**.</span></span> <span data-ttu-id="2df46-199">Elija la definición de compilación de hello creado en un paso anterior.</span><span class="sxs-lookup"><span data-stu-id="2df46-199">Choose hello build definition created in a previous step.</span></span>
2. <span data-ttu-id="2df46-200">En **completado recientemente**, elija la compilación más reciente de Hola y luego seleccione **versión**.</span><span class="sxs-lookup"><span data-stu-id="2df46-200">Under **Recently completed**, choose hello most recent build, then select **Release**.</span></span>
3. <span data-ttu-id="2df46-201">Elija **Sí** toocreate una definición de la versión.</span><span class="sxs-lookup"><span data-stu-id="2df46-201">Choose **Yes** toocreate a release definition.</span></span>
4. <span data-ttu-id="2df46-202">Elija hello **vacía** plantilla, a continuación, seleccione **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2df46-202">Choose hello **Empty** template, then select **Next**.</span></span>
5. <span data-ttu-id="2df46-203">Compruebe la definición de compilación de proyecto y de origen Hola se rellenan con el proyecto.</span><span class="sxs-lookup"><span data-stu-id="2df46-203">Verify hello project and source build definition are populated with your project.</span></span>
6. <span data-ttu-id="2df46-204">Seleccione hello **implementación continua** casilla de verificación, a continuación, seleccione **crear**.</span><span class="sxs-lookup"><span data-stu-id="2df46-204">Select hello **Continuous deployment** check box, then select **Create**.</span></span>
7. <span data-ttu-id="2df46-205">Seleccione cuadro de lista desplegable de hello siguiente demasiado**+ agregar tareas** y elija *agregar una fase de implementación de grupo*.</span><span class="sxs-lookup"><span data-stu-id="2df46-205">Select hello drop-down box next too**+ Add tasks** and choose *Add a deployment group phase*.</span></span>
    
    ![Agregar definición de tarea toorelease en Team Services](media/tutorial-vsts-iis-cicd/add_release_task.png)

8. <span data-ttu-id="2df46-207">Elija **agregar** siguiente demasiado**Deploy(Preview) de aplicación Web de IIS**, a continuación, seleccione **cerrar**.</span><span class="sxs-lookup"><span data-stu-id="2df46-207">Choose **Add** next too**IIS Web App Deploy(Preview)**, then select **Close**.</span></span>
9. <span data-ttu-id="2df46-208">Seleccione hello **ejecutar en el grupo de implementación** tarea primaria.</span><span class="sxs-lookup"><span data-stu-id="2df46-208">Select hello **Run on deployment group** parent task.</span></span>
    1. <span data-ttu-id="2df46-209">Para **grupo de implementación**, seleccione el grupo de implementación de hello creado anteriormente, como *myIIS*.</span><span class="sxs-lookup"><span data-stu-id="2df46-209">For **Deployment Group**, select hello deployment group you created earlier, such as *myIIS*.</span></span>
    2. <span data-ttu-id="2df46-210">Hola **etiquetas de máquina** cuadro, seleccione **agregar** y elija hello *web* etiqueta.</span><span class="sxs-lookup"><span data-stu-id="2df46-210">In hello **Machine tags** box, select **Add** and choose hello *web* tag.</span></span>
    
    ![Tarea del grupo de implementación de la definición de versión en IIS](media/tutorial-vsts-iis-cicd/release_definition_iis.png)
 
11. <span data-ttu-id="2df46-212">Seleccione hello **implementar: implementación de aplicación Web IIS** tooconfigure tarea IIS instancia opciones del siguiente modo:</span><span class="sxs-lookup"><span data-stu-id="2df46-212">Select hello **Deploy: IIS Web App Deploy** task tooconfigure your IIS instance settings as follows:</span></span>
    1. <span data-ttu-id="2df46-213">En **Nombre del sitio web**, escriba *Sitio web predeterminado*.</span><span class="sxs-lookup"><span data-stu-id="2df46-213">For **Website Name**, enter *Default Web Site*.</span></span>
    2. <span data-ttu-id="2df46-214">Deje Hola todas las otras configuraciones predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="2df46-214">Leave all hello other default settings.</span></span>
12. <span data-ttu-id="2df46-215">Elija **Guardar** y, a continuación, seleccione **Aceptar** dos veces.</span><span class="sxs-lookup"><span data-stu-id="2df46-215">Choose **Save**, then select **OK** twice.</span></span>


## <a name="create-a-release-and-publish"></a><span data-ttu-id="2df46-216">Creación de una versión y publicación</span><span class="sxs-lookup"><span data-stu-id="2df46-216">Create a release and publish</span></span>
<span data-ttu-id="2df46-217">Ahora puede enviar el paquete de implementación web como una nueva versión.</span><span class="sxs-lookup"><span data-stu-id="2df46-217">You can now push your web deploy package as a new release.</span></span> <span data-ttu-id="2df46-218">Este paso se comunica con el agente de hello en cada instancia que forma parte del grupo de implementación de hello, inserta web Hola implementar paquete, a continuación, configura la aplicación web IIS toorun Hola actualizado.</span><span class="sxs-lookup"><span data-stu-id="2df46-218">This step communicates with hello agent on each instance that is part of hello deployment group, pushes hello web deploy package, then configures IIS toorun hello updated web application.</span></span>

1. <span data-ttu-id="2df46-219">En la definición de versión, seleccione **+ Versión** y, a continuación, elija **Crear versión**.</span><span class="sxs-lookup"><span data-stu-id="2df46-219">In your release definition, select **+ Release**, then choose **Create Release**.</span></span>
2. <span data-ttu-id="2df46-220">Compruebe que la compilación más reciente de hello está seleccionado en la lista desplegable de hello, junto con **la implementación automatizada: después de la creación de la versión**.</span><span class="sxs-lookup"><span data-stu-id="2df46-220">Verify that hello latest build is selected in hello drop-down list, along with **Automated deployment: After release creation**.</span></span> <span data-ttu-id="2df46-221">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2df46-221">Select **Create**.</span></span>
3. <span data-ttu-id="2df46-222">El encabezado pequeño aparece a través de la parte superior de saludo de la definición de la versión, como *versión 'Versión 1' se ha creado*.</span><span class="sxs-lookup"><span data-stu-id="2df46-222">A small banner appears across hello top of your release definition, such as *Release 'Release-1' has been created*.</span></span> <span data-ttu-id="2df46-223">Vínculo de la versión de Hola seleccione.</span><span class="sxs-lookup"><span data-stu-id="2df46-223">Select hello release link.</span></span>
4. <span data-ttu-id="2df46-224">Abra hello **registros** pestaña progreso de versión de hello toowatch.</span><span class="sxs-lookup"><span data-stu-id="2df46-224">Open hello **Logs** tab toowatch hello release progress.</span></span>
    
    ![Versión e inserción del paquete de implementación web de Team Services correctas](media/tutorial-vsts-iis-cicd/successful_release.png)

5. <span data-ttu-id="2df46-226">Una vez completada la versión de hello, abra un explorador web y escriba Hola pública PII dirección de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2df46-226">After hello release is complete, open a web browser and enter hello public IIP address of your VM.</span></span> <span data-ttu-id="2df46-227">Se está ejecutando la aplicación web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="2df46-227">Your ASP.NET web application is running.</span></span>

    ![Aplicación web ASP.NET en ejecución en la máquina virtual de IIS](media/tutorial-vsts-iis-cicd/running_web_app.png)


## <a name="test-hello-whole-cicd-pipeline"></a><span data-ttu-id="2df46-229">Probar Hola todo CI/CD canalización</span><span class="sxs-lookup"><span data-stu-id="2df46-229">Test hello whole CI/CD pipeline</span></span>
<span data-ttu-id="2df46-230">Con la aplicación web que se ejecuta en IIS, intente ahora canalización de hello todo CI/CD.</span><span class="sxs-lookup"><span data-stu-id="2df46-230">With your web application running on IIS, now try hello whole CI/CD pipeline.</span></span> <span data-ttu-id="2df46-231">Después de realizar un cambio en Visual Studio y la confirmación se desencadena el código, una compilación, lo que, a continuación, desencadena una versión del sitio web actualizado implementar tooIIS de paquete:</span><span class="sxs-lookup"><span data-stu-id="2df46-231">After you make a change in Visual Studio and commit your code, a build is triggered which then triggers a release of your updated web deploy package tooIIS:</span></span>

1. <span data-ttu-id="2df46-232">En Visual Studio, abra hello **el Explorador de soluciones** ventana.</span><span class="sxs-lookup"><span data-stu-id="2df46-232">In Visual Studio, open hello **Solution Explorer** window.</span></span>
2. <span data-ttu-id="2df46-233">Navegue tooand abrir *myWebApp | Vistas | Inicio | Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="2df46-233">Navigate tooand open *myWebApp | Views | Home | Index.cshtml*</span></span>
3. <span data-ttu-id="2df46-234">Editar la línea 6 tooread:</span><span class="sxs-lookup"><span data-stu-id="2df46-234">Edit line 6 tooread:</span></span>

    `<h1>ASP.NET with VSTS and CI/CD!</h1>`

4. <span data-ttu-id="2df46-235">Guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="2df46-235">Save hello file.</span></span>
5. <span data-ttu-id="2df46-236">Abra hello **Team Explorer** (ventana), seleccione hello *myWebApp* del proyecto, y luego elija **cambios**.</span><span class="sxs-lookup"><span data-stu-id="2df46-236">Open hello **Team Explorer** window, select hello *myWebApp* project, then choose **Changes**.</span></span>
6. <span data-ttu-id="2df46-237">Escriba un mensaje de confirmación, como *pruebas CI/CD canalización*, a continuación, elija **todos de confirmación y sincronización** desde el menú desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="2df46-237">Enter a commit message, such as *Testing CI/CD pipeline*, then choose **Commit All and Sync** from hello drop-down menu.</span></span>
7. <span data-ttu-id="2df46-238">En el área de trabajo de Team Services, se desencadena una nueva compilación de confirmación de código de hello.</span><span class="sxs-lookup"><span data-stu-id="2df46-238">In Team Services workspace, a new build is triggered from hello code commit.</span></span> 
    - <span data-ttu-id="2df46-239">Elija **Compilación y versión** y, a continuación, seleccione **Compilaciones**.</span><span class="sxs-lookup"><span data-stu-id="2df46-239">Choose **Build & Release**, then select **Builds**.</span></span> 
    - <span data-ttu-id="2df46-240">Elija la definición de compilación y vuelva a seleccionar hello **en cola & ejecución** toowatch de compilación como Hola compilación progresa.</span><span class="sxs-lookup"><span data-stu-id="2df46-240">Choose your build definition, then select hello **Queued & running** build toowatch as hello build progresses.</span></span>
9. <span data-ttu-id="2df46-241">Una vez Hola compilación es correcta, se desencadena una nueva versión.</span><span class="sxs-lookup"><span data-stu-id="2df46-241">Once hello build is successful, a new release is triggered.</span></span>
    - <span data-ttu-id="2df46-242">Elija **compilar & versión**, a continuación, **versiones** toosee Hola WebDeploy paquete inserta tooyour IIS VM.</span><span class="sxs-lookup"><span data-stu-id="2df46-242">Choose **Build & Release**, then **Releases** toosee hello web deploy package pushed tooyour IIS VM.</span></span> 
    - <span data-ttu-id="2df46-243">Seleccione hello **actualizar** iconos de estado de hello tooupdate.</span><span class="sxs-lookup"><span data-stu-id="2df46-243">Select hello **Refresh** icon tooupdate hello status.</span></span> <span data-ttu-id="2df46-244">Cuando Hola *entornos* columna muestra una marca de verificación verde, versión de Hola ha implementado correctamente tooIIS.</span><span class="sxs-lookup"><span data-stu-id="2df46-244">When hello *Environments* column shows a green check mark, hello release has successfully deployed tooIIS.</span></span>
11. <span data-ttu-id="2df46-245">aplicar los cambios de toosee, actualice el sitio Web IIS en un explorador.</span><span class="sxs-lookup"><span data-stu-id="2df46-245">toosee your changes applied, refresh your IIS website in a browser.</span></span>

    ![Aplicación web ASP.NET en ejecución en una máquina virtual de IIS desde la canalización CI/CD](media/tutorial-vsts-iis-cicd/running_web_app_cicd.png)


## <a name="next-steps"></a><span data-ttu-id="2df46-247">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2df46-247">Next steps</span></span>

<span data-ttu-id="2df46-248">En este tutorial, creó una aplicación web ASP.NET en Team Services y compilación configurado y versión definiciones toodeploy nuevo web implementación paquetes tooIIS en cada confirmación de código.</span><span class="sxs-lookup"><span data-stu-id="2df46-248">In this tutorial, you created an ASP.NET web application in Team Services and configured build and release definitions toodeploy new web deploy packages tooIIS on each code commit.</span></span> <span data-ttu-id="2df46-249">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="2df46-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2df46-250">Publicar un proyecto de Team Services de tooa de aplicación web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="2df46-250">Publish an ASP.NET web application tooa Team Services project</span></span>
> * <span data-ttu-id="2df46-251">Crear una definición de compilación que se desencadena mediante confirmaciones de código</span><span class="sxs-lookup"><span data-stu-id="2df46-251">Create a build definition that is triggered by code commits</span></span>
> * <span data-ttu-id="2df46-252">Instalar y configurar IIS en una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="2df46-252">Install and configure IIS on a virtual machine in Azure</span></span>
> * <span data-ttu-id="2df46-253">Agregar grupo de implementación de tooa de instancia IIS de hello en Team Services</span><span class="sxs-lookup"><span data-stu-id="2df46-253">Add hello IIS instance tooa deployment group in Team Services</span></span>
> * <span data-ttu-id="2df46-254">Crear un nuevo web de versión definición toopublish implementar paquetes tooIIS</span><span class="sxs-lookup"><span data-stu-id="2df46-254">Create a release definition toopublish new web deploy packages tooIIS</span></span>
> * <span data-ttu-id="2df46-255">Probar Hola CI/CD canalización</span><span class="sxs-lookup"><span data-stu-id="2df46-255">Test hello CI/CD pipeline</span></span>

<span data-ttu-id="2df46-256">Avanzar toohello siguiente tutorial toolearn cómo toosecure un servidor web con certificados SSL.</span><span class="sxs-lookup"><span data-stu-id="2df46-256">Advance toohello next tutorial toolearn how toosecure a web server with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2df46-257">Protección de un servidor web con SSL</span><span class="sxs-lookup"><span data-stu-id="2df46-257">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)