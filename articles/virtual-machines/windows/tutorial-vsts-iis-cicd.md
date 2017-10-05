---
title: "Creación de una canalización de CI/CD en Azure con Team Services | Microsoft Docs"
description: "Obtenga información acerca de cómo crear una canalización de Visual Studio Team Services para integración y entrega continuas, que implementa una aplicación web en IIS en una máquina virtual Windows"
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
ms.openlocfilehash: a587f58fad2ec74c7633823c4d34f900e7c01f7e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-continuous-integration-pipeline-with-visual-studio-team-services-and-iis"></a><span data-ttu-id="b5c78-103">Creación de una canalización de integración continua con Visual Studio Team Services e IIS</span><span class="sxs-lookup"><span data-stu-id="b5c78-103">Create a continuous integration pipeline with Visual Studio Team Services and IIS</span></span>
<span data-ttu-id="b5c78-104">Para automatizar las fases de creación, prueba e implementación del desarrollo de la aplicación, puede utilizar una canalización de integración e implementación continua (CI/CD).</span><span class="sxs-lookup"><span data-stu-id="b5c78-104">To automate the build, test, and deployment phases of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="b5c78-105">En este tutorial se creará una canalización CI/CD utilizando Visual Studio Team Services y una máquina virtual Windows en Azure que ejecuta IIS.</span><span class="sxs-lookup"><span data-stu-id="b5c78-105">In this tutorial, you create a CI/CD pipeline using Visual Studio Team Services and a Windows virtual machine (VM) in Azure that runs IIS.</span></span> <span data-ttu-id="b5c78-106">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="b5c78-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b5c78-107">Publicar una aplicación web ASP.NET en un proyecto de Team Services</span><span class="sxs-lookup"><span data-stu-id="b5c78-107">Publish an ASP.NET web application to a Team Services project</span></span>
> * <span data-ttu-id="b5c78-108">Crear una definición de compilación que se desencadena mediante confirmaciones de código</span><span class="sxs-lookup"><span data-stu-id="b5c78-108">Create a build definition that is triggered by code commits</span></span>
> * <span data-ttu-id="b5c78-109">Instalar y configurar IIS en una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="b5c78-109">Install and configure IIS on a virtual machine in Azure</span></span>
> * <span data-ttu-id="b5c78-110">Agregar la instancia de IIS a un grupo de implementación de Team Services</span><span class="sxs-lookup"><span data-stu-id="b5c78-110">Add the IIS instance to a deployment group in Team Services</span></span>
> * <span data-ttu-id="b5c78-111">Crear una definición de versión para publicar nuevos paquetes de implementación en IIS</span><span class="sxs-lookup"><span data-stu-id="b5c78-111">Create a release definition to publish new web deploy packages to IIS</span></span>
> * <span data-ttu-id="b5c78-112">Prueba de la canalización de CI/CD</span><span class="sxs-lookup"><span data-stu-id="b5c78-112">Test the CI/CD pipeline</span></span>

<span data-ttu-id="b5c78-113">Para realizar este tutorial es necesaria la versión 3.6 del módulo de Azure PowerShell, o cualquier versión posterior.</span><span class="sxs-lookup"><span data-stu-id="b5c78-113">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="b5c78-114">Ejecute `Get-Module -ListAvailable AzureRM` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="b5c78-114">Run `Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="b5c78-115">Si necesita actualizarla, consulte [Instalación del módulo de Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="b5c78-115">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="create-project-in-team-services"></a><span data-ttu-id="b5c78-116">Crear el proyecto en Team Services</span><span class="sxs-lookup"><span data-stu-id="b5c78-116">Create project in Team Services</span></span>
<span data-ttu-id="b5c78-117">Visual Studio Team Services permite una colaboración y desarrollo sencillos sin mantener una solución de administración de código local.</span><span class="sxs-lookup"><span data-stu-id="b5c78-117">Visual Studio Team Services allows for easy collaboration and development without maintaining an on-premises code management solution.</span></span> <span data-ttu-id="b5c78-118">Team Services proporciona pruebas de código en la nube, compilación y visión de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b5c78-118">Team Services provides cloud code testing, build, and application insights.</span></span> <span data-ttu-id="b5c78-119">Puede elegir el repositorio de control de versiones y el IDE que mejor se adapten a su desarrollo de código.</span><span class="sxs-lookup"><span data-stu-id="b5c78-119">You can choose a version control repo and IDE that best fits your code development.</span></span> <span data-ttu-id="b5c78-120">Para este tutorial, puede usar una cuenta gratuita para crear una aplicación web ASP.NET básica y la canalización de CI/CD.</span><span class="sxs-lookup"><span data-stu-id="b5c78-120">For this tutorial, you can use a free account to create a basic ASP.NET web app and CI/CD pipeline.</span></span> <span data-ttu-id="b5c78-121">Si no dispone de una cuenta de Team Services, [cree una](http://go.microsoft.com/fwlink/?LinkId=307137).</span><span class="sxs-lookup"><span data-stu-id="b5c78-121">If you do not already have a Team Services account, [create one](http://go.microsoft.com/fwlink/?LinkId=307137).</span></span>

<span data-ttu-id="b5c78-122">Para administrar el proceso de confirmación de código, las definiciones de compilación y las definiciones de versión, cree un proyecto en Team Services del modo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b5c78-122">To manage the code commit process, build definitions, and release definitions, create a project in Team Services as follows:</span></span>

1. <span data-ttu-id="b5c78-123">Abra el panel de Team Services en un explorador web y elija **Nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-123">Open your Team Services dashboard in a web browser and choose **New project**.</span></span>
2. <span data-ttu-id="b5c78-124">Escriba *myWebApp* como **Nombre del proyecto**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-124">Enter *myWebApp* for the **Project name**.</span></span> <span data-ttu-id="b5c78-125">Deje todos los demás valores predeterminados para usar el control de versiones *Git* y el proceso de elementos de trabajo *Agile*.</span><span class="sxs-lookup"><span data-stu-id="b5c78-125">Leave all other default values to use *Git* version control and *Agile* work item process.</span></span>
3. <span data-ttu-id="b5c78-126">Elija la opción de **Compartir con** *Miembros del equipo* y, a continuación, seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-126">Choose the option to **Share with** *Team Members*, then select **Create**.</span></span>
5. <span data-ttu-id="b5c78-127">Una vez creado el proyecto, elija la opción **Inicializar con un archivo Léame o gitignore** y, a continuación, **Inicializar**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-127">Once your project has been created, choose the option to **Initialize with a README or gitignore**, then **Initialize**.</span></span>
6. <span data-ttu-id="b5c78-128">En el proyecto nuevo, elija **Paneles** en la parte superior y, a continuación, seleccione **Abrir en Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-128">Inside your new project, choose **Dashboards** across the top, then select **Open in Visual Studio**.</span></span>


## <a name="create-aspnet-web-application"></a><span data-ttu-id="b5c78-129">Creación de una aplicación web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b5c78-129">Create ASP.NET web application</span></span>
<span data-ttu-id="b5c78-130">En el paso anterior, creó un proyecto en Team Services.</span><span class="sxs-lookup"><span data-stu-id="b5c78-130">In the previous step, you created a project in Team Services.</span></span> <span data-ttu-id="b5c78-131">El último paso abre el proyecto nuevo en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b5c78-131">The final step opens your new project in Visual Studio.</span></span> <span data-ttu-id="b5c78-132">Las confirmaciones de código se administran en la ventana **Team Explorer**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-132">You manage your code commits in the **Team Explorer** window.</span></span> <span data-ttu-id="b5c78-133">Cree una copia local del nuevo proyecto y, a continuación, cree una aplicación web ASP.NET a partir de una plantilla, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="b5c78-133">Create a local copy of your new project, then create an ASP.NET web application from a template as follows:</span></span>

1. <span data-ttu-id="b5c78-134">Seleccione **Clonar** para crear un repositorio de git local del proyecto de Team Services.</span><span class="sxs-lookup"><span data-stu-id="b5c78-134">Select **Clone** to create a local git repo of your Team Services project.</span></span>
    
    ![Clonación del repositorio del proyecto de Team Services](media/tutorial-vsts-iis-cicd/clone_repo.png)

2. <span data-ttu-id="b5c78-136">En **Soluciones**, seleccione **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-136">Under **Solutions**, select **New**.</span></span>

    ![Creación de la solución de aplicación web](media/tutorial-vsts-iis-cicd/new_solution.png)

3. <span data-ttu-id="b5c78-138">Seleccione plantillas **Web** y, a continuación, elija la plantilla **Aplicación Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-138">Select **Web** templates, and then choose the **ASP.NET Web Application** template.</span></span>
    1. <span data-ttu-id="b5c78-139">Escriba un nombre para la aplicación, como *myWebApp*y desactive la casilla **Crear directorio para la solución**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-139">Enter a name for your application, such as *myWebApp*, and uncheck the box for **Create directory for solution**.</span></span>
    2. <span data-ttu-id="b5c78-140">Si la opción está disponible, desactive la casilla para **Agregar Application Insights al proyecto**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-140">If the option is available, uncheck the box to **Add Application Insights to project**.</span></span> <span data-ttu-id="b5c78-141">Application Insights precisa que autorice la aplicación web con Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b5c78-141">Application Insights requires you to authorize your web application with Azure Application Insights.</span></span> <span data-ttu-id="b5c78-142">Para simplificar en este tutorial, omita este proceso.</span><span class="sxs-lookup"><span data-stu-id="b5c78-142">To keep it simple in this tutorial, skip this process.</span></span>
    3. <span data-ttu-id="b5c78-143">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-143">Select **OK**.</span></span>
4. <span data-ttu-id="b5c78-144">Elija **MVC** en la lista de plantillas.</span><span class="sxs-lookup"><span data-stu-id="b5c78-144">Choose **MVC** from the template list.</span></span>
    1. <span data-ttu-id="b5c78-145">Seleccione **Cambiar autenticación**, elija **Sin autenticación** y, a continuación, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-145">Select **Change Authentication**, choose **No Authentication**, then select **OK**.</span></span>
    2. <span data-ttu-id="b5c78-146">Seleccione **Aceptar** para crear la solución.</span><span class="sxs-lookup"><span data-stu-id="b5c78-146">Select **OK** to create your solution.</span></span>
5. <span data-ttu-id="b5c78-147">En la ventana **Team Explorer**, elija **Cambios**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-147">In the **Team Explorer** window, choose **Changes**.</span></span>

    ![Confirmación de los cambios locales en el repositorio de git de Team Services](media/tutorial-vsts-iis-cicd/commit_changes.png)

6. <span data-ttu-id="b5c78-149">En el cuadro de texto de confirmación, escriba un mensaje como *Confirmación inicial*.</span><span class="sxs-lookup"><span data-stu-id="b5c78-149">In the commit text box, enter a message such as *Initial commit*.</span></span> <span data-ttu-id="b5c78-150">Elija **Confirmar todos y sincronizar** en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="b5c78-150">Choose **Commit All and Sync** from the drop-down menu.</span></span>


## <a name="create-build-definition"></a><span data-ttu-id="b5c78-151">Creación de la definición de compilación</span><span class="sxs-lookup"><span data-stu-id="b5c78-151">Create build definition</span></span>
<span data-ttu-id="b5c78-152">En Team Services, se utiliza una definición de compilación para describir cómo se debe compilar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b5c78-152">In Team Services, you use a build definition to outline how your application should be built.</span></span> <span data-ttu-id="b5c78-153">En este tutorial, creamos una definición básica que toma el código fuente, compila la solución y, a continuación, crea un paquete de implementación web que podemos usar para ejecutar la aplicación web en un servidor IIS.</span><span class="sxs-lookup"><span data-stu-id="b5c78-153">In this tutorial, we create a basic definition that takes our source code, builds the solution, then creates web deploy package we can use to run the web app on an IIS server.</span></span>

1. <span data-ttu-id="b5c78-154">En el proyecto de Team Services, elija **Compilación y versión** en la parte superior y, a continuación, seleccione **Compilaciones**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-154">In your Team Services project, choose **Build & Release** across the top, then select **Builds**.</span></span>
3. <span data-ttu-id="b5c78-155">Seleccione **+ Nueva definición**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-155">Select **+ New definition**.</span></span>
4. <span data-ttu-id="b5c78-156">Elija la plantilla **ASP.NET (versión preliminar)** y seleccione **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-156">Choose the **ASP.NET (PREVIEW)** template and select **Apply**.</span></span>
5. <span data-ttu-id="b5c78-157">Deje todos los valores predeterminados de la tarea.</span><span class="sxs-lookup"><span data-stu-id="b5c78-157">Leave all the default task values.</span></span> <span data-ttu-id="b5c78-158">En **Obtener fuentes**, asegúrese de que el repositorio *myWebApp* y la bifurcación *master* están seleccionados.</span><span class="sxs-lookup"><span data-stu-id="b5c78-158">Under **Get sources**, ensure that the *myWebApp* repository and *master* branch are selected.</span></span>

    ![Creación de la definición de compilación en el proyecto de Team Services](media/tutorial-vsts-iis-cicd/create_build_definition.png)

6. <span data-ttu-id="b5c78-160">En la pestaña **Desencadenadores**, mueva el control deslizante para **Habilitar este desencadenador** a *Habilitado*.</span><span class="sxs-lookup"><span data-stu-id="b5c78-160">On the **Triggers** tab, move the slider for **Enable this trigger** to *Enabled*.</span></span>
7. <span data-ttu-id="b5c78-161">Guarde la definición de compilación y ponga en cola una compilación nueva seleccionando **Guardar y poner en cola** y, a continuación, **Guardar y poner en cola** de nuevo.</span><span class="sxs-lookup"><span data-stu-id="b5c78-161">Save the build definition and queue a new build by selecting **Save & queue** , then **Save & queue** again.</span></span> <span data-ttu-id="b5c78-162">Deje los valores predeterminados y seleccione **Poner en cola**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-162">Leave the defaults and select **Queue**.</span></span>

<span data-ttu-id="b5c78-163">Observe cómo la compilación se programa en un agente hospedado y después comienza la compilación.</span><span class="sxs-lookup"><span data-stu-id="b5c78-163">Watch as the build is scheduled on a hosted agent, then begins to build.</span></span> <span data-ttu-id="b5c78-164">La salida es similar a la del ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b5c78-164">The output is similar to the following example:</span></span>

![Compilación correcta del proyecto de Team Services](media/tutorial-vsts-iis-cicd/successful_build.png)


## <a name="create-virtual-machine"></a><span data-ttu-id="b5c78-166">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="b5c78-166">Create virtual machine</span></span>
<span data-ttu-id="b5c78-167">Para proporcionar una plataforma para ejecutar la aplicación web ASP.NET, necesita una máquina virtual Windows que ejecute IIS.</span><span class="sxs-lookup"><span data-stu-id="b5c78-167">To provide a platform to run your ASP.NET web app, you need a Windows virtual machine that runs IIS.</span></span> <span data-ttu-id="b5c78-168">Team Services utiliza un agente para interactuar con la instancia de IIS cuando confirma el código y se desencadenan compilaciones.</span><span class="sxs-lookup"><span data-stu-id="b5c78-168">Team Services uses an agent to interact with the IIS instance as you commit code and builds are triggered.</span></span>

<span data-ttu-id="b5c78-169">Cree una máquina virtual Windows Server 2016 mediante [este script de ejemplo](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b5c78-169">Create a Windows Server 2016 VM using [this script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json).</span></span> <span data-ttu-id="b5c78-170">El script tarda unos minutos en ejecutarse y crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b5c78-170">It takes a few minutes for the script to run and create the VM.</span></span> <span data-ttu-id="b5c78-171">Una vez creada la máquina virtual, abra el puerto 80 para el tráfico web con [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermresourcegroup) como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="b5c78-171">Once the VM has been created, open port 80 for web traffic with [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermresourcegroup) as follows:</span></span>

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

<span data-ttu-id="b5c78-172">Para conectarse a la máquina virtual, obtenga la dirección IP pública con [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="b5c78-172">To connect to your VM, obtain the public IP address with [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) as follows:</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName $resourceGroup | Select IpAddress
```

<span data-ttu-id="b5c78-173">Cree una sesión de escritorio remoto a la máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="b5c78-173">Create a remote desktop session to your VM:</span></span>

```cmd
mstsc /v:<publicIpAddress>
```

<span data-ttu-id="b5c78-174">En la máquina virtual, abra un símbolo del sistema **PowerShell de administrador**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-174">On the VM, open an **Administrator PowerShell** command prompt.</span></span> <span data-ttu-id="b5c78-175">Instale IIS y las características de .NET necesarias como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="b5c78-175">Install IIS and required .NET features as follows:</span></span>

```powershell
Install-WindowsFeature Web-Server,Web-Asp-Net45,NET-Framework-Features
```


## <a name="create-deployment-group"></a><span data-ttu-id="b5c78-176">Creación de un grupo de implementación</span><span class="sxs-lookup"><span data-stu-id="b5c78-176">Create deployment group</span></span>
<span data-ttu-id="b5c78-177">Para enviar el paquete de implementación de la web al servidor IIS, defina un grupo de implementación en Team Services.</span><span class="sxs-lookup"><span data-stu-id="b5c78-177">To push out the web deploy package to the IIS server, you define a deployment group in Team Services.</span></span> <span data-ttu-id="b5c78-178">Este grupo permite especificar los servidores que son el destino de nuevas compilaciones cuando confirme código en Team Services y las compilaciones se hayan completado.</span><span class="sxs-lookup"><span data-stu-id="b5c78-178">This group allows you to specify which servers are the target of new builds as you commit code to Team Services and builds are completed.</span></span>

1. <span data-ttu-id="b5c78-179">En Team Services, elija **Compilación y versión** y, a continuación, seleccione **Grupos de implementación**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-179">In Team Services, choose **Build & Release** and then select **Deployment groups**.</span></span>
2. <span data-ttu-id="b5c78-180">Elija **Agregar grupo de implementación**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-180">Choose **Add Deployment group**.</span></span>
3. <span data-ttu-id="b5c78-181">Escriba un nombre para el grupo, como *myIIS* y, a continuación, seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-181">Enter a name for the group, such as *myIIS*, then select **Create**.</span></span>
4. <span data-ttu-id="b5c78-182">En la sección **Registrar máquinas**, asegúrese de que *Windows* está seleccionado y, a continuación, active la casilla para **Usar un token de acceso personal en el script para la autenticación**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-182">In the **Register machines** section, ensure *Windows* is selected, then check the box to **Use a personal access token in the script for authentication**.</span></span>
5. <span data-ttu-id="b5c78-183">Seleccione **Copiar script en el portapapeles**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-183">Select **Copy script to clipboard**.</span></span>


### <a name="add-iis-vm-to-the-deployment-group"></a><span data-ttu-id="b5c78-184">Incorporación de la máquina virtual de IIS al grupo de implementación</span><span class="sxs-lookup"><span data-stu-id="b5c78-184">Add IIS VM to the deployment group</span></span>
<span data-ttu-id="b5c78-185">Con el grupo de implementación creado, agregue cada instancia de IIS al grupo.</span><span class="sxs-lookup"><span data-stu-id="b5c78-185">With the deployment group created, add each IIS instance to the group.</span></span> <span data-ttu-id="b5c78-186">Team Services genera un script que se descarga y configura un agente en la máquina virtual que recibe los nuevos paquetes de implementación web y, a continuación, los aplica a IIS.</span><span class="sxs-lookup"><span data-stu-id="b5c78-186">Team Services generates a script that downloads and configures an agent on the VM that receives new web deploy packages then applies it to IIS.</span></span>

1. <span data-ttu-id="b5c78-187">En la sesión de **PowerShell de administrador** en la máquina virtual, pegue y ejecute el script copiado desde Team Services.</span><span class="sxs-lookup"><span data-stu-id="b5c78-187">Back in the **Administrator PowerShell** session on your VM, paste and run the script copied from Team Services.</span></span>
2. <span data-ttu-id="b5c78-188">Cuando se le solicite configurar etiquetas para el agente, elija *S* y escriba *web*.</span><span class="sxs-lookup"><span data-stu-id="b5c78-188">When prompted to configure tags for the agent, choose *Y* and enter *web*.</span></span>
3. <span data-ttu-id="b5c78-189">Cuando se le solicite la cuenta de usuario, presione *Intro* para aceptar los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="b5c78-189">When prompted for the user account, press *Return* to accept the defaults.</span></span>
4. <span data-ttu-id="b5c78-190">Espere a que termine el script con el mensaje *El servicio vstsagent.account.computername se inició correctamente*.</span><span class="sxs-lookup"><span data-stu-id="b5c78-190">Wait for the script to finish with a message *Service vstsagent.account.computername started successfully*.</span></span>
5. <span data-ttu-id="b5c78-191">En la página **Grupos de implementación** del menú **Compilación y versión**, abra el grupo de implementación *myIIS*.</span><span class="sxs-lookup"><span data-stu-id="b5c78-191">In the **Deployment groups** page of the **Build & Release** menu, open the *myIIS* deployment group.</span></span> <span data-ttu-id="b5c78-192">Compruebe que aparece la máquina virtual en la pestaña **Máquinas**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-192">On the **Machines** tab, verify that your VM is listed.</span></span>

    ![Máquina virtual agregada correctamente al grupo de implementación de Team Services](media/tutorial-vsts-iis-cicd/deployment_group.png)


## <a name="create-release-definition"></a><span data-ttu-id="b5c78-194">Creación de la definición de versión</span><span class="sxs-lookup"><span data-stu-id="b5c78-194">Create release definition</span></span>
<span data-ttu-id="b5c78-195">Para publicar las compilaciones, se crea una definición de versión en Team Services.</span><span class="sxs-lookup"><span data-stu-id="b5c78-195">To publish your builds, you create a release definition in Team Services.</span></span> <span data-ttu-id="b5c78-196">Esta definición se desencadena automáticamente por una compilación correcta de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b5c78-196">This definition is triggered automatically by a successful build of your application.</span></span> <span data-ttu-id="b5c78-197">Elija el grupo de implementación al que enviar el paquete de implementación web y defina la configuración de IIS adecuada.</span><span class="sxs-lookup"><span data-stu-id="b5c78-197">You choose the deployment group to push your web deploy package to, and define the appropriate IIS settings.</span></span>

1. <span data-ttu-id="b5c78-198">Elija **Compilación y versión** y, a continuación, seleccione **Compilaciones**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-198">Choose **Build & Release**, then select **Builds**.</span></span> <span data-ttu-id="b5c78-199">Elija la definición de compilación que creó en un paso anterior.</span><span class="sxs-lookup"><span data-stu-id="b5c78-199">Choose the build definition created in a previous step.</span></span>
2. <span data-ttu-id="b5c78-200">En **Completados recientemente**, elija la compilación más reciente y luego seleccione **Versión**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-200">Under **Recently completed**, choose the most recent build, then select **Release**.</span></span>
3. <span data-ttu-id="b5c78-201">Elija **Sí** para crear una definición de versión.</span><span class="sxs-lookup"><span data-stu-id="b5c78-201">Choose **Yes** to create a release definition.</span></span>
4. <span data-ttu-id="b5c78-202">Elija la plantilla **Vacía** y, a continuación, seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-202">Choose the **Empty** template, then select **Next**.</span></span>
5. <span data-ttu-id="b5c78-203">Compruebe que el proyecto y la definición de compilación se rellenan con los datos del proyecto.</span><span class="sxs-lookup"><span data-stu-id="b5c78-203">Verify the project and source build definition are populated with your project.</span></span>
6. <span data-ttu-id="b5c78-204">Seleccione la casilla de verificación **Implementación continua** y, a continuación, seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-204">Select the **Continuous deployment** check box, then select **Create**.</span></span>
7. <span data-ttu-id="b5c78-205">Seleccione el cuadro de lista desplegable junto a **+ Agregar tareas** y elija *Agregar una fase de grupo de implementación*.</span><span class="sxs-lookup"><span data-stu-id="b5c78-205">Select the drop-down box next to **+ Add tasks** and choose *Add a deployment group phase*.</span></span>
    
    ![Incorporación de la tarea a la definición de versión en Team Services](media/tutorial-vsts-iis-cicd/add_release_task.png)

8. <span data-ttu-id="b5c78-207">Elija **Agregar** junto a **Implementación de aplicaciones web de IIS (versión preliminar)** y, a continuación, seleccione **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-207">Choose **Add** next to **IIS Web App Deploy(Preview)**, then select **Close**.</span></span>
9. <span data-ttu-id="b5c78-208">Seleccione la tarea primaria **Ejecutar en el grupo de implementación**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-208">Select the **Run on deployment group** parent task.</span></span>
    1. <span data-ttu-id="b5c78-209">Para **Grupo de implementación**, seleccione el grupo de implementación que creó anteriormente, como *myIIS*.</span><span class="sxs-lookup"><span data-stu-id="b5c78-209">For **Deployment Group**, select the deployment group you created earlier, such as *myIIS*.</span></span>
    2. <span data-ttu-id="b5c78-210">En el cuadro de texto **Etiquetas de máquina**, seleccione **Agregar** y elija la etiqueta *web*.</span><span class="sxs-lookup"><span data-stu-id="b5c78-210">In the **Machine tags** box, select **Add** and choose the *web* tag.</span></span>
    
    ![Tarea del grupo de implementación de la definición de versión en IIS](media/tutorial-vsts-iis-cicd/release_definition_iis.png)
 
11. <span data-ttu-id="b5c78-212">Seleccione la tarea **Implementar: implementación de aplicaciones web de IIS** para configurar la instancia de IIS del modo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b5c78-212">Select the **Deploy: IIS Web App Deploy** task to configure your IIS instance settings as follows:</span></span>
    1. <span data-ttu-id="b5c78-213">En **Nombre del sitio web**, escriba *Sitio web predeterminado*.</span><span class="sxs-lookup"><span data-stu-id="b5c78-213">For **Website Name**, enter *Default Web Site*.</span></span>
    2. <span data-ttu-id="b5c78-214">Deje el resto de los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="b5c78-214">Leave all the other default settings.</span></span>
12. <span data-ttu-id="b5c78-215">Elija **Guardar** y, a continuación, seleccione **Aceptar** dos veces.</span><span class="sxs-lookup"><span data-stu-id="b5c78-215">Choose **Save**, then select **OK** twice.</span></span>


## <a name="create-a-release-and-publish"></a><span data-ttu-id="b5c78-216">Creación de una versión y publicación</span><span class="sxs-lookup"><span data-stu-id="b5c78-216">Create a release and publish</span></span>
<span data-ttu-id="b5c78-217">Ahora puede enviar el paquete de implementación web como una nueva versión.</span><span class="sxs-lookup"><span data-stu-id="b5c78-217">You can now push your web deploy package as a new release.</span></span> <span data-ttu-id="b5c78-218">Este paso comunica con el agente de cada instancia que forma parte del grupo de implementación, envía el paquete de implementación web y configura IIS para que ejecute la aplicación web actualizada.</span><span class="sxs-lookup"><span data-stu-id="b5c78-218">This step communicates with the agent on each instance that is part of the deployment group, pushes the web deploy package, then configures IIS to run the updated web application.</span></span>

1. <span data-ttu-id="b5c78-219">En la definición de versión, seleccione **+ Versión** y, a continuación, elija **Crear versión**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-219">In your release definition, select **+ Release**, then choose **Create Release**.</span></span>
2. <span data-ttu-id="b5c78-220">Compruebe que está seleccionada la última compilación en la lista desplegable, junto con **Implementación automatizada: después de crear la versión**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-220">Verify that the latest build is selected in the drop-down list, along with **Automated deployment: After release creation**.</span></span> <span data-ttu-id="b5c78-221">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-221">Select **Create**.</span></span>
3. <span data-ttu-id="b5c78-222">Aparecerá un pequeño banner en la parte superior de la definición de la versión, como *Se ha creado la versión 'Versión 1'*.</span><span class="sxs-lookup"><span data-stu-id="b5c78-222">A small banner appears across the top of your release definition, such as *Release 'Release-1' has been created*.</span></span> <span data-ttu-id="b5c78-223">Seleccione el enlace de la versión.</span><span class="sxs-lookup"><span data-stu-id="b5c78-223">Select the release link.</span></span>
4. <span data-ttu-id="b5c78-224">Abra la pestaña **Registros** para ver el progreso de la versión.</span><span class="sxs-lookup"><span data-stu-id="b5c78-224">Open the **Logs** tab to watch the release progress.</span></span>
    
    ![Versión e inserción del paquete de implementación web de Team Services correctas](media/tutorial-vsts-iis-cicd/successful_release.png)

5. <span data-ttu-id="b5c78-226">Una vez completada la versión, abra un explorador web y escriba la dirección IP pública de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b5c78-226">After the release is complete, open a web browser and enter the public IIP address of your VM.</span></span> <span data-ttu-id="b5c78-227">Se está ejecutando la aplicación web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b5c78-227">Your ASP.NET web application is running.</span></span>

    ![Aplicación web ASP.NET en ejecución en la máquina virtual de IIS](media/tutorial-vsts-iis-cicd/running_web_app.png)


## <a name="test-the-whole-cicd-pipeline"></a><span data-ttu-id="b5c78-229">Prueba de la canalización CI/CD</span><span class="sxs-lookup"><span data-stu-id="b5c78-229">Test the whole CI/CD pipeline</span></span>
<span data-ttu-id="b5c78-230">Con la aplicación web en ejecución en IIS, ahora se probará toda la canalización CI/CD.</span><span class="sxs-lookup"><span data-stu-id="b5c78-230">With your web application running on IIS, now try the whole CI/CD pipeline.</span></span> <span data-ttu-id="b5c78-231">Después de realizar un cambio en Visual Studio y confirmar el código, se desencadena una compilación que a su vez desencadena una versión del paquete de implementación actualizada en IIS:</span><span class="sxs-lookup"><span data-stu-id="b5c78-231">After you make a change in Visual Studio and commit your code, a build is triggered which then triggers a release of your updated web deploy package to IIS:</span></span>

1. <span data-ttu-id="b5c78-232">En Visual Studio, abra la ventana **Explorador de soluciones**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-232">In Visual Studio, open the **Solution Explorer** window.</span></span>
2. <span data-ttu-id="b5c78-233">Vaya a *myWebApp | Vistas | Inicio | Index.cshtml* y ábralo.</span><span class="sxs-lookup"><span data-stu-id="b5c78-233">Navigate to and open *myWebApp | Views | Home | Index.cshtml*</span></span>
3. <span data-ttu-id="b5c78-234">Edite la línea 6 así:</span><span class="sxs-lookup"><span data-stu-id="b5c78-234">Edit line 6 to read:</span></span>

    `<h1>ASP.NET with VSTS and CI/CD!</h1>`

4. <span data-ttu-id="b5c78-235">Guarde el archivo .</span><span class="sxs-lookup"><span data-stu-id="b5c78-235">Save the file.</span></span>
5. <span data-ttu-id="b5c78-236">Abra la ventana **Team Explorer**, seleccione el proyecto *myWebApp* y luego elija **Cambios**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-236">Open the **Team Explorer** window, select the *myWebApp* project, then choose **Changes**.</span></span>
6. <span data-ttu-id="b5c78-237">Escriba un mensaje de confirmación, como *Pruebas canalización CI/CD* y, a continuación, elija **Confirmar todos y sincronizar** en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="b5c78-237">Enter a commit message, such as *Testing CI/CD pipeline*, then choose **Commit All and Sync** from the drop-down menu.</span></span>
7. <span data-ttu-id="b5c78-238">En el área de trabajo de Team Services, se desencadena una nueva compilación desde la confirmación de código.</span><span class="sxs-lookup"><span data-stu-id="b5c78-238">In Team Services workspace, a new build is triggered from the code commit.</span></span> 
    - <span data-ttu-id="b5c78-239">Elija **Compilación y versión** y, a continuación, seleccione **Compilaciones**.</span><span class="sxs-lookup"><span data-stu-id="b5c78-239">Choose **Build & Release**, then select **Builds**.</span></span> 
    - <span data-ttu-id="b5c78-240">Elija la definición de compilación y, a continuación, seleccione **En cola y en ejecución** para ver el progreso de la compilación.</span><span class="sxs-lookup"><span data-stu-id="b5c78-240">Choose your build definition, then select the **Queued & running** build to watch as the build progresses.</span></span>
9. <span data-ttu-id="b5c78-241">Una vez que la compilación es correcta, se desencadena una nueva versión.</span><span class="sxs-lookup"><span data-stu-id="b5c78-241">Once the build is successful, a new release is triggered.</span></span>
    - <span data-ttu-id="b5c78-242">Elija **Compilación y versión** y, a continuación, seleccione **Compilaciones** para ver el paquete de implementación web enviado a la máquina virtual de IIS.</span><span class="sxs-lookup"><span data-stu-id="b5c78-242">Choose **Build & Release**, then **Releases** to see the web deploy package pushed to your IIS VM.</span></span> 
    - <span data-ttu-id="b5c78-243">Seleccione el icono **Actualizar** para actualizar el estado.</span><span class="sxs-lookup"><span data-stu-id="b5c78-243">Select the **Refresh** icon to update the status.</span></span> <span data-ttu-id="b5c78-244">Cuando la columna *Entornos* muestra una marca de verificación verde, la versión se ha implementado correctamente en IIS.</span><span class="sxs-lookup"><span data-stu-id="b5c78-244">When the *Environments* column shows a green check mark, the release has successfully deployed to IIS.</span></span>
11. <span data-ttu-id="b5c78-245">Para ver los cambios aplicados, actualice el sitio web IIS en un explorador.</span><span class="sxs-lookup"><span data-stu-id="b5c78-245">To see your changes applied, refresh your IIS website in a browser.</span></span>

    ![Aplicación web ASP.NET en ejecución en una máquina virtual de IIS desde la canalización CI/CD](media/tutorial-vsts-iis-cicd/running_web_app_cicd.png)


## <a name="next-steps"></a><span data-ttu-id="b5c78-247">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b5c78-247">Next steps</span></span>

<span data-ttu-id="b5c78-248">En este tutorial, ha creado una aplicación web ASP.NET en Team Services y configurado la compilación y definición de versión para que se implementen nuevos paquetes de implementación web en IIS en cada confirmación de código.</span><span class="sxs-lookup"><span data-stu-id="b5c78-248">In this tutorial, you created an ASP.NET web application in Team Services and configured build and release definitions to deploy new web deploy packages to IIS on each code commit.</span></span> <span data-ttu-id="b5c78-249">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="b5c78-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b5c78-250">Publicar una aplicación web ASP.NET en un proyecto de Team Services</span><span class="sxs-lookup"><span data-stu-id="b5c78-250">Publish an ASP.NET web application to a Team Services project</span></span>
> * <span data-ttu-id="b5c78-251">Crear una definición de compilación que se desencadena mediante confirmaciones de código</span><span class="sxs-lookup"><span data-stu-id="b5c78-251">Create a build definition that is triggered by code commits</span></span>
> * <span data-ttu-id="b5c78-252">Instalar y configurar IIS en una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="b5c78-252">Install and configure IIS on a virtual machine in Azure</span></span>
> * <span data-ttu-id="b5c78-253">Agregar la instancia de IIS a un grupo de implementación de Team Services</span><span class="sxs-lookup"><span data-stu-id="b5c78-253">Add the IIS instance to a deployment group in Team Services</span></span>
> * <span data-ttu-id="b5c78-254">Crear una definición de versión para publicar nuevos paquetes de implementación en IIS</span><span class="sxs-lookup"><span data-stu-id="b5c78-254">Create a release definition to publish new web deploy packages to IIS</span></span>
> * <span data-ttu-id="b5c78-255">Prueba de la canalización de CI/CD</span><span class="sxs-lookup"><span data-stu-id="b5c78-255">Test the CI/CD pipeline</span></span>

<span data-ttu-id="b5c78-256">Pase al siguiente tutorial para aprender a proteger un servidor web con certificados SSL.</span><span class="sxs-lookup"><span data-stu-id="b5c78-256">Advance to the next tutorial to learn how to secure a web server with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b5c78-257">Protección de un servidor web con SSL</span><span class="sxs-lookup"><span data-stu-id="b5c78-257">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)