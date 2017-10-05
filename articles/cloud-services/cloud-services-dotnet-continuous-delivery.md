---
title: Entrega continua para Cloud Services con TFS en Azure | Microsoft Doc
description: "Aprenda a configurar la entrega continua para las aplicaciones en la nube de Azure. Ejemplos de código para las instrucciones de línea de comandos de MSBuild y scripts PowerShell."
services: cloud-services
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 4f3c93c6-5c82-4779-9d19-7404a01e82ca
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/12/2017
ms.author: kraigb
ms.openlocfilehash: 0979722b9ec715e91825c7aba74657451df6e83f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="continuous-delivery-for-cloud-services-in-azure"></a><span data-ttu-id="6f0e1-104">Entrega continua para Servicios en la nube de Azure</span><span class="sxs-lookup"><span data-stu-id="6f0e1-104">Continuous Delivery for Cloud Services in Azure</span></span>
<span data-ttu-id="6f0e1-105">El proceso que se describe en este artículo muestra cómo se configura la entrega continua para las aplicaciones en la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-105">The process described in this article shows you how to set up continuous delivery for Azure cloud apps.</span></span> <span data-ttu-id="6f0e1-106">Este proceso le permite crear automáticamente paquetes e implementar el paquete en Azure cada vez que se proteja el código.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-106">This process enables you to automatically create packages and deploy the package to Azure after every code check-in.</span></span> <span data-ttu-id="6f0e1-107">El proceso de compilación del paquete que se describe en este artículo es equivalente al comando **Package** en Visual Studio y los pasos de publicación son equivalentes al comando **Publish** en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-107">The package build process described in this article is equivalent to the **Package** command in Visual Studio, and the publishing steps are equivalent to the **Publish** command in Visual Studio.</span></span>
<span data-ttu-id="6f0e1-108">El artículo abarca los métodos que usaría para crear un servidor de compilación con instrucciones de línea de comandos de MSBuild y scripts de Windows PowerShell; además, demuestra también cómo configurar de manera opcional las definiciones de Visual Studio Team Foundation Server - Team Build para usar los comandos de MSBuild y los scripts de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-108">The article covers the methods you would use to create a build server with MSBuild command-line statements and Windows PowerShell scripts, and it also demonstrates how to optionally configure Visual Studio Team Foundation Server - Team Build definitions to use the MSBuild commands and PowerShell scripts.</span></span> <span data-ttu-id="6f0e1-109">El proceso se puede personalizar para su entorno de compilación y los entornos de destino de Azure.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-109">The process is customizable for your build environment and Azure target environments.</span></span>

<span data-ttu-id="6f0e1-110">Para hacerlo de manera más fácil, puede también usar Visual Studio Team Services, una versión de TFS que se hospeda en Azure.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-110">You can also use Visual Studio Team Services, a version of TFS that is hosted in Azure, to do this more easily.</span></span> 

<span data-ttu-id="6f0e1-111">Antes de comenzar, debe publicar su aplicación desde Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-111">Before you start, you should publish your application from Visual Studio.</span></span>
<span data-ttu-id="6f0e1-112">Esto asegurará que todos los recursos estén disponibles e inicializados cuando intente automatizar el proceso de publicación.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-112">This will ensure that all the resources are available and initialized when you attempt to automate the publication process.</span></span>

## <a name="1-configure-the-build-server"></a><span data-ttu-id="6f0e1-113">1: Configuración del servidor de compilación</span><span class="sxs-lookup"><span data-stu-id="6f0e1-113">1: Configure the Build Server</span></span>
<span data-ttu-id="6f0e1-114">Antes de crear un paquete de Azure con MSBuild, debe instalar el software y las herramientas necesarias en el servidor de compilación.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-114">Before you can create an Azure package by using MSBuild, you must install the required software and tools on the build server.</span></span>

<span data-ttu-id="6f0e1-115">No es necesario instalar Visual Studio en el servidor de compilación.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-115">Visual Studio is not required to be installed on the build server.</span></span> <span data-ttu-id="6f0e1-116">Si desea usar el servicio de Team Foundation Build para administrar el servidor de compilación, siga las instrucciones que aparecen en el documento [Configurar el Servicio de Team Foundation Build][Team Foundation Build Service].</span><span class="sxs-lookup"><span data-stu-id="6f0e1-116">If you want to use Team Foundation Build Service to manage your build server, follow the instructions in the [Team Foundation Build Service][Team Foundation Build Service] documentation.</span></span>

1. <span data-ttu-id="6f0e1-117">En el servidor de compilación, instale [.NET Framework 4.5.2][.NET Framework 4.5.2], que incluye MSBuild.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-117">On the build server, install the [.NET Framework 4.5.2][.NET Framework 4.5.2], which includes MSBuild.</span></span>
2. <span data-ttu-id="6f0e1-118">Instale las [Herramientas de creación de Azure para .NET](https://azure.microsoft.com/develop/net/).</span><span class="sxs-lookup"><span data-stu-id="6f0e1-118">Install the latest [Azure Authoring Tools for .NET](https://azure.microsoft.com/develop/net/).</span></span>
3. <span data-ttu-id="6f0e1-119">Instale las [Bibliotecas de Azure para .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span><span class="sxs-lookup"><span data-stu-id="6f0e1-119">Install the [Azure Libraries for .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span></span>
4. <span data-ttu-id="6f0e1-120">Copie el archivo Microsoft.WebApplication.targets desde una instalación de Visual Studio en el servidor de compilación.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-120">Copy the Microsoft.WebApplication.targets file from a Visual Studio installation to the build server.</span></span>

   <span data-ttu-id="6f0e1-121">En un equipo con Visual Studio instalado, este archivo se encuentra en el directorio C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-121">On a computer with Visual Studio installed, this file is located in the directory C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications.</span></span> <span data-ttu-id="6f0e1-122">Debe copiarlo en el mismo directorio en el servidor de compilación.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-122">You should copy it to the same directory on the build server.</span></span>
5. <span data-ttu-id="6f0e1-123">Instale las [Herramientas de Azure para Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="6f0e1-123">Install the [Azure Tools for Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span></span>

## <a name="2-build-a-package-using-msbuild-commands"></a><span data-ttu-id="6f0e1-124">2 Compilación de un paquete con comandos de MSBuild</span><span class="sxs-lookup"><span data-stu-id="6f0e1-124">2: Build a Package using MSBuild Commands</span></span>
<span data-ttu-id="6f0e1-125">En esta sección se describe cómo construir un comando de MSBuild que compila un paquete de Azure.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-125">This section describes how to construct an MSBuild command that builds an Azure package.</span></span> <span data-ttu-id="6f0e1-126">Ejecute este paso en el servidor de compilación para comprobar que todo está configurado correctamente y que el comando MSBuild hace lo que usted quiere.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-126">Run this step on the build server to verify that everything is configured correctly and that the MSBuild command does what you want it to do.</span></span> <span data-ttu-id="6f0e1-127">Puede agregar esta línea de comandos a scripts de compilación existentes en el servidor de compilación, o puede usar la línea de comandos en una definición de compilación de TFS, tal como se describe en la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-127">You can either add this command line to existing build scripts on the build server, or you can use the command line in a TFS Build Definition, as described in the next section.</span></span> <span data-ttu-id="6f0e1-128">Para obtener más información acerca de los parámetros de línea de comandos y MSBuild, consulte [Referencia de la línea de comandos de MSBuild](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="6f0e1-128">For more information about command-line parameters and MSBuild, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>

1. <span data-ttu-id="6f0e1-129">Si Visual Studio está instalado en el servidor de compilación, ubique y elija **Símbolo del sistema de Visual Studio** en la carpeta **Visual Studio Tools** de Windows.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-129">If Visual Studio is installed on the build server, locate and choose **Visual Studio Command Prompt** in the **Visual Studio Tools** folder in Windows.</span></span>

   <span data-ttu-id="6f0e1-130">Si Visual Studio no está instalado en el servidor de compilación, abra un símbolo del sistema y asegúrese de que se pueda tener acceso a MSBuild.exe en la ruta.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-130">If Visual Studio is not installed on the build server, open a command prompt and make sure that MSBuild.exe is accessible on the path.</span></span> <span data-ttu-id="6f0e1-131">MSBuild se instala con .NET Framework en la ruta %WINDIR%\\Microsoft.NET\\Framework\\*Version*.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-131">MSBuild is installed with the .NET Framework in the path %WINDIR%\\Microsoft.NET\\Framework\\*Version*.</span></span> <span data-ttu-id="6f0e1-132">Por ejemplo, para agregar MSBuild.exe a la variable de entorno PATH cuando tiene instalado .NET Framework 4, escriba el siguiente comando en el símbolo del sistema:</span><span class="sxs-lookup"><span data-stu-id="6f0e1-132">For example, to add MSBuild.exe to the PATH environment variable when you have .NET Framework 4 installed, type the following command at the command prompt:</span></span>

       set PATH=%PATH%;"C:\Windows\Microsoft.NET\Framework\v4.0.30319"
2. <span data-ttu-id="6f0e1-133">En el símbolo del sistema, navegue hasta la carpeta que contiene el archivo de proyecto de Azure que desea compilar.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-133">At the command prompt, navigate to the folder containing the Azure project file that you want to build.</span></span>
3. <span data-ttu-id="6f0e1-134">Ejecute MSBuild con la opción /target:Publish como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="6f0e1-134">Run MSBuild with the /target:Publish option as in the following example:</span></span>

       MSBuild /target:Publish

   <span data-ttu-id="6f0e1-135">Esta opción se puede abreviar como /t:Publish.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-135">This option can be abbreviated as /t:Publish.</span></span> <span data-ttu-id="6f0e1-136">La opción /t:Publish en MSBuild no debe confundirse con los comandos de publicación disponibles en Visual Studio cuando tiene instalado el SDK de Azure.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-136">The /t:Publish option in MSBuild should not be confused with the Publish commands available in Visual Studio when you have the Azure SDK installed.</span></span> <span data-ttu-id="6f0e1-137">La opción /t:Publish solo compila los paquetes de Azure.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-137">The /t:Publish option only builds the Azure packages.</span></span> <span data-ttu-id="6f0e1-138">No implementa los paquetes como lo hacen los comandos de publicación en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-138">It does not deploy the packages as the Publish commands in Visual Studio do.</span></span>

   <span data-ttu-id="6f0e1-139">De manera opcional, puede especificar el nombre del proyecto como un parámetro de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-139">Optionally, you can specify the project name as an MSBuild parameter.</span></span> <span data-ttu-id="6f0e1-140">Si no se especifica, se utiliza el directorio actual.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-140">If not specified, the current directory is used.</span></span> <span data-ttu-id="6f0e1-141">Para más información acerca de las opciones de línea de comandos de MSBuild, consulte [Referencia de la línea de comandos de MSBuild1](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="6f0e1-141">For more information about MSBuild command line options, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>
4. <span data-ttu-id="6f0e1-142">Busque el resultado.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-142">Locate the output.</span></span> <span data-ttu-id="6f0e1-143">De manera predeterminada, este comando crea un directorio en relación con la carpeta raíz para el proyecto, como por ejemplo *ProjectDir*\\bin\\*Configuration*\\app.publish\\.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-143">By default, this command creates a directory in relation to the root folder for the project, such as *ProjectDir*\\bin\\*Configuration*\\app.publish\\.</span></span> <span data-ttu-id="6f0e1-144">Al compilar un proyecto de Azure, se generan dos archivos: el archivo del paquete mismo y el archivo de configuración que lo acompaña:</span><span class="sxs-lookup"><span data-stu-id="6f0e1-144">When you build an Azure project, you generate two files, the package file itself and the accompanying configuration file:</span></span>

   * <span data-ttu-id="6f0e1-145">Project.cspkg</span><span class="sxs-lookup"><span data-stu-id="6f0e1-145">Project.cspkg</span></span>
   * <span data-ttu-id="6f0e1-146">ServiceConfiguration.*TargetProfile*.cscfg</span><span class="sxs-lookup"><span data-stu-id="6f0e1-146">ServiceConfiguration.*TargetProfile*.cscfg</span></span>

   <span data-ttu-id="6f0e1-147">De manera predeterminada, cada proyecto de Azure incluye un archivo de configuración del servicio (archivo .cscfg) para las compilaciones locales (depuración) y otro para las compilaciones en la nube (ensayo o producción), pero puede agregar o quitar archivos de configuración del servicio según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-147">By default, each Azure project includes one service configuration file (.cscfg file) for local (debugging) builds and another for cloud (staging or production) builds, but you can add or remove service configuration files as needed.</span></span> <span data-ttu-id="6f0e1-148">Cuando compila un paquete dentro de Visual Studio, se le preguntará cuál archivo de configuración del servicio se debe incluir junto con el paquete.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-148">When you build a package within Visual Studio, you will be asked which service configuration file to include alongside the package.</span></span>
5. <span data-ttu-id="6f0e1-149">Especifique el archivo de configuración del servicio.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-149">Specify the service configuration file.</span></span> <span data-ttu-id="6f0e1-150">Cuando compila un paquete con MSBuild, el archivo de configuración del servicio local se incluye de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-150">When you build a package by using MSBuild, the local service configuration file is included by default.</span></span> <span data-ttu-id="6f0e1-151">Para incluir un archivo de configuración del servicio diferente, establezca la propiedad TargetProfile del comando de MSBuild, como se muestra en el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6f0e1-151">To include a different service configuration file, set the TargetProfile property of the MSBuild command, as in the following example:</span></span>

       MSBuild /t:Publish /p:TargetProfile=Cloud
6. <span data-ttu-id="6f0e1-152">Especifique la ubicación para el resultado.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-152">Specify the location for the output.</span></span> <span data-ttu-id="6f0e1-153">Establezca la ruta mediante la opción /p:PublishDir=*Directory*\\, incluido el separador de barra diagonal inversa final, como en el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6f0e1-153">Set the path by using the /p:PublishDir=*Directory*\\ option, including the trailing backslash separator, as in the following example:</span></span>

       MSBuild /target:Publish /p:PublishDir=\\myserver\drops\

   <span data-ttu-id="6f0e1-154">Después de que haya construido y probado una línea de comandos de MSBuild adecuada para compilar sus proyectos y combinarlos en un paquete de Azure, puede agregar esta línea de comandos a sus scripts de compilación.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-154">Once you've constructed and tested an appropriate MSBuild command line to build your projects and combine them into an Azure package, you can add this command line to your build scripts.</span></span> <span data-ttu-id="6f0e1-155">Si su servidor de compilación usa scripts personalizados, este proceso dependerá de los detalles de su proceso personalizado de compilación.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-155">If your build server uses custom scripts, this process will depend on the specifics of your custom build process.</span></span> <span data-ttu-id="6f0e1-156">Si va a usar TFS como un entorno de compilación, entonces puede seguir las instrucciones del paso siguiente para agregar la compilación del paquete de Azure a su proceso de compilación.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-156">If you are using TFS as a build environment, then you can follow the instructions in the next step to add the Azure package build to your build process.</span></span>

## <a name="3-build-a-package-using-tfs-team-build"></a><span data-ttu-id="6f0e1-157">3: Compilación de un paquete con TFS Team Build</span><span class="sxs-lookup"><span data-stu-id="6f0e1-157">3: Build a Package using TFS Team Build</span></span>
<span data-ttu-id="6f0e1-158">Si tiene Team Foundation Server (TFS) configurado como un controlador de compilación y el servidor de compilación configurado como una máquina de compilación de TFS, entonces puede, opcionalmente, configurar una compilación automatizada para su paquete de Azure.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-158">If you have Team Foundation Server (TFS) set up as a build controller and the build server set up as a TFS build machine, then you can optionally set up an automated build for your Azure package.</span></span> <span data-ttu-id="6f0e1-159">Para obtener información sobre cómo configurar y usar el servidor de Team Foundation como un sistema de compilación, consulte [Escalar horizontalmente el sistema de compilación][Scale out your build system].</span><span class="sxs-lookup"><span data-stu-id="6f0e1-159">For information on how to set up and use Team Foundation server as a build system, see [Scale out your build system][Scale out your build system].</span></span> <span data-ttu-id="6f0e1-160">En particular, el procedimiento siguiente asume que ha configurado el servidor de compilación, tal como se ha descrito en [Implementar y configurar un servidor de compilación][Deploy and configure a build server], y que ha creado un proyecto de equipo y un proyecto de servicio en la nube en el proyecto en equipo.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-160">In particular, the following procedure assumes that you have configured your build server as described in [Deploy and configure a build server][Deploy and configure a build server], and that you have created a team project, created a cloud service project in the team project.</span></span>

<span data-ttu-id="6f0e1-161">Para configurar TFS a fin de compilar paquetes de Azure, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="6f0e1-161">To configure TFS to build Azure packages, perform the following steps:</span></span>

1. <span data-ttu-id="6f0e1-162">En Visual Studio, en el equipo de desarrollo, en el menú Ver, elija **Team Explorer** o seleccione Ctrl+\\, Ctrl+M.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-162">In Visual Studio on your development computer, on the View menu, choose **Team Explorer**, or choose Ctrl+\\, Ctrl+M.</span></span> <span data-ttu-id="6f0e1-163">En la ventana Team Explorer, expanda el nodo **Compilaciones** o elija la página **Compilaciones** y, a continuación, seleccione **Definición de nueva compilación**.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-163">In the Team Explorer window, expand the **Builds** node or choose the **Builds** page, and choose **New Build Definition**.</span></span>

   ![Opción Nueva definición de compilación][0]
2. <span data-ttu-id="6f0e1-165">Haga clic en la pestaña **Desencadenador** y especifique las condiciones deseadas para cuando desea que se compile el paquete.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-165">Choose the **Trigger** tab, and specify the desired conditions for when you want the package to be built.</span></span> <span data-ttu-id="6f0e1-166">Por ejemplo, especifique **Integración continua** para compilar el paquete cada vez que se produce una protección del control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-166">For example, specify **Continuous Integration** to build the package whenever a source control check-in occurs.</span></span>
3. <span data-ttu-id="6f0e1-167">Elija la pestaña **Configuración de origen** y asegúrese de que la carpeta del proyecto se muestra en la columna **Carpeta de control de código fuente** y de que el estado es **Activo**.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-167">Choose the **Source Settings** tab, and make sure your project folder is listed in the **Source Control Folder** column, and the status is **Active**.</span></span>
4. <span data-ttu-id="6f0e1-168">Seleccione la pestaña **Valores predeterminados de compilación** y, en el controlador de compilación, compruebe el nombre del servidor de compilación.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-168">Choose the **Build Defaults** tab, and under Build controller, verify the name of the build server.</span></span>  <span data-ttu-id="6f0e1-169">Además, seleccione la opción **Copiar el resultado de la compilación en la siguiente carpeta** de entrega y especifique la ubicación de destino deseada.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-169">Also, choose the option **Copy build output to the following drop folder** and specify the desired drop location.</span></span>
5. <span data-ttu-id="6f0e1-170">Elija la pestaña **Process** . En la pestaña Proceso, elija la plantilla predeterminada, en **Compilación**, seleccione el proyecto si no está ya seleccionado y expanda la sección **Avanzado** en la sección **Compilación** de la cuadrícula.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-170">Choose the **Process** tab. On the Process tab, choose the default template, under **Build**, choose the project if it is not already selected, and expand the **Advanced** section in the **Build** section of the grid.</span></span>
6. <span data-ttu-id="6f0e1-171">Seleccione **Argumentos de MSBuild**y establezca los argumentos adecuados de la línea de comandos de MSBuild como se describe en el paso 2 anterior.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-171">Choose **MSBuild Arguments**, and set the appropriate MSBuild command line arguments as described in Step 2 above.</span></span> <span data-ttu-id="6f0e1-172">Por ejemplo, escriba **/t:Publish /p:PublishDir=\\\\myserver\\drops\\** para compilar un paquete y copiar los archivos del paquete en la ubicación \\\\myserver\\drops\\:</span><span class="sxs-lookup"><span data-stu-id="6f0e1-172">For example, enter **/t:Publish /p:PublishDir=\\\\myserver\\drops\\** to build a package and copy the package files to the location \\\\myserver\\drops\\:</span></span>

   ![Argumentos de MSBuild][2]

   > [!NOTE]
   > <span data-ttu-id="6f0e1-174">La copia de los archivos en un recurso compartido público facilita la implementación manual de los paquetes desde su equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-174">Copying the files to a public share makes it easier to manually deploy the packages from your development computer.</span></span>
7. <span data-ttu-id="6f0e1-175">Pruebe el éxito del paso de compilación protegiendo un cambio en su proyecto o ponga en cola una compilación nueva.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-175">Test the success of your build step by checking in a change to your project, or queue up a new build.</span></span> <span data-ttu-id="6f0e1-176">Para poner en cola una compilación nueva, en Team Explorer, haga clic con el botón derecho en **Todas las definiciones** de compilación y, a continuación, seleccione **Poner nueva compilación en cola**.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-176">To queue up a new build, in the Team Explorer, right-click **All Build Definitions,** and then choose **Queue New Build**.</span></span>

## <a name="4-publish-a-package-using-a-powershell-script"></a><span data-ttu-id="6f0e1-177">4: Publicación de un paquete con un script de PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f0e1-177">4: Publish a Package using a PowerShell Script</span></span>
<span data-ttu-id="6f0e1-178">En esta sección se describen los pasos para construir un script de Windows PowerShell que publicará el resultado del paquete de aplicaciones en la nube en Azure con la ayuda de parámetros opcionales.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-178">This section describes how to construct a Windows PowerShell script that will publish the Cloud app package output to Azure using optional parameters.</span></span> <span data-ttu-id="6f0e1-179">Este script puede llamarse después del paso de compilación en su automatización de compilación personalizada.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-179">This script can be called after the build step in your custom build automation.</span></span> <span data-ttu-id="6f0e1-180">También puede llamarse desde las actividades de flujo de trabajo de la Plantilla de procesos en Visual Studio TFS Team Build.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-180">It can also be called from Process Template workflow activities in Visual Studio TFS Team Build.</span></span>

1. <span data-ttu-id="6f0e1-181">Instale los [cmdlets de Azure PowerShell][Azure PowerShell cmdlets] (versión 0.6.1 o superior).</span><span class="sxs-lookup"><span data-stu-id="6f0e1-181">Install the [Azure PowerShell cmdlets][Azure PowerShell cmdlets] (v0.6.1 or higher).</span></span>
   <span data-ttu-id="6f0e1-182">Durante la fase de instalación del cmdlet, seleccione instalar como complemento.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-182">During the cmdlet setup phase, choose to install as a snap-in.</span></span> <span data-ttu-id="6f0e1-183">Tenga en cuenta que esta versión oficialmente compatible reemplaza la versión anterior que se ofrece mediante CodePlex, aunque las versiones anteriores tenían la numeración 2.x.x.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-183">Note that this officially supported version replaces the older version offered through CodePlex, although the previous versions were numbered 2.x.x.</span></span>
2. <span data-ttu-id="6f0e1-184">Inicie Azure PowerShell mediante el menú Inicio o la página de inicio.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-184">Start Azure PowerShell using the Start menu or Start page.</span></span> <span data-ttu-id="6f0e1-185">Si inicia de esta manera, se cargarán los cmdlets de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-185">If you start in this way, the Azure PowerShell cmdlets will be loaded.</span></span>
3. <span data-ttu-id="6f0e1-186">A la solicitud de PowerShell, compruebe que se cargan los cmdlets de PowerShell al escribir el comando parcial `Get-Azure` y, a continuación, presionar la tecla TAB para completar la instrucción.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-186">At the PowerShell prompt, verify that the PowerShell cmdlets are loaded by entering the partial command `Get-Azure` and then pressing the Tab key for statement completion.</span></span>

   <span data-ttu-id="6f0e1-187">Si presiona varias veces la tecla TAB, debiera ver diversos comandos de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-187">If you press the Tab key repeatedly, you should see various Azure PowerShell commands.</span></span>
4. <span data-ttu-id="6f0e1-188">Verifique que se puede conectar a su suscripción de Azure al importar su información de suscripción desde el archivo .publishsettings.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-188">Verify that you can connect to your Azure subscription by importing your subscription information from the .publishsettings file.</span></span>

   `Import-AzurePublishSettingsFile c:\scripts\WindowsAzure\default.publishsettings`

   <span data-ttu-id="6f0e1-189">Luego, escriba el comando.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-189">Then enter the command</span></span>

   `Get-AzureSubscription`

   <span data-ttu-id="6f0e1-190">Se muestra información sobre su suscripción.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-190">This shows information about your subscription.</span></span> <span data-ttu-id="6f0e1-191">Verifique que todo esté correcto.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-191">Verify that everything is correct.</span></span>
5. <span data-ttu-id="6f0e1-192">Guarde la plantilla de script que aparece al final de este artículo en la carpeta de scripts como c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-192">Save the script template provided at the end of this article to your scripts folder as c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.</span></span>
6. <span data-ttu-id="6f0e1-193">Revise la sección de parámetros del script.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-193">Review the parameters section of the script.</span></span> <span data-ttu-id="6f0e1-194">Agregue o modifique cualquiera de los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-194">Add or modify any default values.</span></span> <span data-ttu-id="6f0e1-195">Estos valores siempre pueden omitirse al pasar parámetros explícitos.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-195">These values can always be overridden by passing in explicit parameters.</span></span>
7. <span data-ttu-id="6f0e1-196">Asegúrese de que haya cuentas de almacenamiento y de servicio en la nube válidas creadas en su suscripción que se puedan abordar mediante el script de publicación.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-196">Ensure there are valid cloud service and storage accounts created in your subscription that can be targeted by the publish script.</span></span> <span data-ttu-id="6f0e1-197">Se usará la cuenta de almacenamiento (almacenamiento de blobs) para cargar y almacenar temporalmente el paquete de implementación y el archivo de configuración mientras se crea la implementación.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-197">The storage account (blob storage) will be used to upload and temporarily store the deployment package and config file while the deployment is being created.</span></span>

   * <span data-ttu-id="6f0e1-198">Para crear un servicio en la nube, puede llamar a este script o usar [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6f0e1-198">To create a new cloud service, you can call this script or use the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6f0e1-199">El nombre del servicio en la nube se usará como prefijo en un nombre de dominio completo y, por este motivo, debe ser único.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-199">The cloud service name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span>

         New-AzureService -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
   * <span data-ttu-id="6f0e1-200">Para crear una nueva cuenta de almacenamiento, puede llamar a este script o usar [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6f0e1-200">To create a new storage account, you can call this script or use the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6f0e1-201">El nombre de la cuenta de almacenamiento se usará como prefijo en un nombre de dominio completo y, por este motivo, debe ser único.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-201">The storage account name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span> <span data-ttu-id="6f0e1-202">Puede intentar usar el mismo nombre que el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-202">You can try using the same name as the cloud service.</span></span>

         New-AzureStorageAccount -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
8. <span data-ttu-id="6f0e1-203">Llame al script directamente desde Azure PowerShell, o conecte este script a su automatización de compilación de host que se produce después de la compilación del paquete.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-203">Call the script directly from Azure PowerShell, or wire up this script to your host build automation to occur after the package build.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="6f0e1-204">El script siempre eliminará o reemplazará sus implementaciones actuales de manera predeterminada si se detectan.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-204">The script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="6f0e1-205">Esto es necesario para habilitar la entrega continua desde la automatización donde no es posible una solicitud del usuario.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-205">This is necessary to enable continuous delivery from automation where no user prompting is possible.</span></span>
   >
   >

   <span data-ttu-id="6f0e1-206">**Escenario de ejemplo 1:** implementación continua en el entorno de ensayo de un servicio:</span><span class="sxs-lookup"><span data-stu-id="6f0e1-206">**Example scenario 1:** continuous deployment to the staging environment of a service:</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Staging -serviceName mycloudservice -storageAccountName mystoragesaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="6f0e1-207">A esto le sigue generalmente una verificación de ejecución de prueba y un intercambio de VIP.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-207">This is typically followed up by test run verification and a VIP swap.</span></span> <span data-ttu-id="6f0e1-208">El intercambio de VIP se puede realizar mediante [Azure Portal](https://portal.azure.com) o con el cmdlet Move-Deployment.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-208">The VIP swap can be done via the [Azure portal](https://portal.azure.com) or by using the Move-Deployment cmdlet.</span></span>

   <span data-ttu-id="6f0e1-209">**Escenario de ejemplo 2:** implementación continua en el entorno de producción de un servicio de prueba dedicado</span><span class="sxs-lookup"><span data-stu-id="6f0e1-209">**Example scenario 2:** continuous deployment to the production environment of a dedicated test service</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Production -enableDeploymentUpgrade 1 -serviceName mycloudservice -storageAccountName mystorageaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="6f0e1-210">**Escritorio remoto:**</span><span class="sxs-lookup"><span data-stu-id="6f0e1-210">**Remote Desktop:**</span></span>

   <span data-ttu-id="6f0e1-211">Si se habilita Escritorio remoto en su proyecto de Azure, necesitará realizar algunos pasos únicos adicionales para asegurarse de que se cargue el certificado de servicio en la nube correcto en todos los servicios en la nube abordados por este script.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-211">If Remote Desktop is enabled in your Azure project you will need to perform additional one-time steps to ensure the correct Cloud Service Certificate is uploaded to all cloud services targeted by this script.</span></span>

   <span data-ttu-id="6f0e1-212">Busque los valores de huella digital del certificado que esperan sus roles.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-212">Locate the certificate thumbprint values expected by your roles.</span></span> <span data-ttu-id="6f0e1-213">Los valores de huella digital son visibles en la sección Certificados del archivo de configuración de la nube (es decir, ServiceConfiguration.Cloud.cscfg).</span><span class="sxs-lookup"><span data-stu-id="6f0e1-213">The thumbprint values are visible in the Certificates section of the cloud config file (i.e. ServiceConfiguration.Cloud.cscfg).</span></span> <span data-ttu-id="6f0e1-214">También son visibles en el cuadro de diálogo Configuración de Escritorio remoto en Visual Studio cuando muestra las opciones y ve el certificado seleccionado.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-214">It is also visible in the Remote Desktop Configuration dialog in Visual Studio when you Show Options and view the selected certificate.</span></span>

       <Certificates>
             <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="C33B6C432C25581601B84C80F86EC2809DC224E8" thumbprintAlgorithm="sha1" />
       </Certificates>

   <span data-ttu-id="6f0e1-215">Cargue los certificados de Escritorio remoto como un paso de configuración único usando el siguiente script de cmdlet:</span><span class="sxs-lookup"><span data-stu-id="6f0e1-215">Upload Remote Desktop certificates as a one-time setup step using the following cmdlet script:</span></span>

       Add-AzureCertificate -serviceName <CLOUDSERVICENAME> -certToDeploy (get-item cert:\CurrentUser\MY\<THUMBPRINT>)

   <span data-ttu-id="6f0e1-216">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6f0e1-216">For example:</span></span>

       Add-AzureCertificate -serviceName 'mytestcloudservice' -certToDeploy (get-item cert:\CurrentUser\MY\C33B6C432C25581601B84C80F86EC2809DC224E8

   <span data-ttu-id="6f0e1-217">Si lo prefiere, puede exportar el archivo de certificado PFX con una clave privada y cargar los certificados en cada servicio en la nube de destino mediante [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6f0e1-217">Alternatively you can export the certificate file PFX with private key and upload certificates to each target cloud service using the [Azure portal](https://portal.azure.com).</span></span>

   <!---
   Fixing broken links for Azure content migration from ACOM to DOCS. I'm unable to find a replacement links, so I'm commenting out this reference for now. The author can investigate in the future. "Read the following article to learn more: http://msdn.microsoft.com/library/windowsazure/gg443832.aspx.
   -->
   <span data-ttu-id="6f0e1-218">**Actualizar implementación frente a Eliminar implementación -\> Nueva implementación**</span><span class="sxs-lookup"><span data-stu-id="6f0e1-218">**Upgrade Deployment vs. Delete Deployment -\> New Deployment**</span></span>

   <span data-ttu-id="6f0e1-219">El script realizará de manera predeterminada una actualización de la implementación ($enableDeploymentUpgrade = 1) cuando no se pasa ningún parámetro o el valor 1 se pasa de manera explícita.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-219">The script will by default perform an Upgrade Deployment ($enableDeploymentUpgrade = 1) when no parameter is passed in or the value 1 is passed explicitly.</span></span> <span data-ttu-id="6f0e1-220">Para las instancias simples, esto tiene la ventaja de tardar menos tiempo que una implementación completa.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-220">For single instances this has the advantage of taking less time than a full deployment.</span></span> <span data-ttu-id="6f0e1-221">Para las instancias que requieren una alta disponibilidad, esto también tiene la ventaja de dejar algunas instancias en ejecución mientras otras se actualizan (recorriendo su dominio de actualización), además de que no se eliminará su VIP.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-221">For instances that require high availability this also has the advantage of leaving some instances running while others are upgraded (walking your update domain), plus your VIP will not be deleted.</span></span>

   <span data-ttu-id="6f0e1-222">La actualización de la implementación se puede deshabilitar en el script ($enableDeploymentUpgrade = 0) o al pasar *-enableDeploymentUpgrade 0* como un parámetro, el cual alterará el comportamiento del script para primero eliminar cualquier implementación existente y luego crear una implementación nueva.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-222">Upgrade Deployment can be disabled in the script ($enableDeploymentUpgrade = 0) or by passing *-enableDeploymentUpgrade 0* as a parameter, which alters the script behavior to first delete any existing deployment and then create a new deployment.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="6f0e1-223">El script siempre eliminará o reemplazará sus implementaciones actuales de manera predeterminada si se detectan.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-223">The script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="6f0e1-224">Esto es necesario para habilitar la entrega continua desde la automatización donde no es posible una solicitud del usuario/operador.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-224">This is necessary to enable continuous delivery from automation where no user/operator prompting is possible.</span></span>
   >
   >

## <a name="5-publish-a-package-using-tfs-team-build"></a><span data-ttu-id="6f0e1-225">5: Publicación de un paquete con TFS Team Build</span><span class="sxs-lookup"><span data-stu-id="6f0e1-225">5: Publish a Package using TFS Team Build</span></span>
<span data-ttu-id="6f0e1-226">Este paso opcional conecta TFS Team Build al script que se creó en el paso 4, el cual controla la publicación de la compilación del paquete en Azure.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-226">This optional step connects TFS Team Build to the script created in step 4, which handles publishing of the package build to Azure.</span></span> <span data-ttu-id="6f0e1-227">Esto conlleva modificar la Plantilla de proceso que usó su definición de compilación, de modo que ejecuta una actividad de publicación al final del flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-227">This entails modifying the Process Template used by your build definition so that it runs a Publish activity at the end of the workflow.</span></span> <span data-ttu-id="6f0e1-228">La actividad de publicación ejecutará su comando de PowerShell al pasar parámetros desde la compilación.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-228">The Publish activity will execute your PowerShell command passing in parameters from the build.</span></span> <span data-ttu-id="6f0e1-229">El resultado de los objetivos de MSBuild y el script de publicación se canalizarán al resultado de la compilación estándar.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-229">Output of the MSBuild targets and publish script will be piped into the standard build output.</span></span>

1. <span data-ttu-id="6f0e1-230">Edite la definición de compilación a cargo de la implementación continua.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-230">Edit the Build Definition responsible for continuous deploy.</span></span>
2. <span data-ttu-id="6f0e1-231">Seleccione la pestaña **Proceso** .</span><span class="sxs-lookup"><span data-stu-id="6f0e1-231">Select the **Process** tab.</span></span>
3. <span data-ttu-id="6f0e1-232">Siga [estas instrucciones](http://msdn.microsoft.com/library/dd647551.aspx) para agregar un proyecto de actividad a la plantilla del proceso de compilación, descargue la plantilla predeterminada, agréguela al proyecto y protéjala.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-232">Follow [these instructions](http://msdn.microsoft.com/library/dd647551.aspx) to add an Activity project for the build process template, download the default template, add it to the project and check it in.</span></span> <span data-ttu-id="6f0e1-233">Asigne un nuevo nombre a la plantilla del proceso de compilación, como AzureBuildProcessTemplate.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-233">Give the build process template a new name, such as AzureBuildProcessTemplate.</span></span>
4. <span data-ttu-id="6f0e1-234">Vuelva a la pestaña **Proceso** y use **Mostrar detalles** para mostrar una lista de las plantillas de proceso de compilación disponibles.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-234">Return to the **Process** tab, and use **Show Details** to show a list of available build process templates.</span></span> <span data-ttu-id="6f0e1-235">Elija el botón **Nuevo...** , vaya al proyecto que acaba de agregar y protéjalo.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-235">Choose the **New...** button, and navigate to the project you just added and checked in.</span></span> <span data-ttu-id="6f0e1-236">Localice la plantilla que acaba de crear y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-236">Locate the template you just created and choose **OK**.</span></span>
5. <span data-ttu-id="6f0e1-237">Abra la Plantilla de proceso seleccionada para editar.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-237">Open the selected Process Template for editing.</span></span> <span data-ttu-id="6f0e1-238">Puede abrirla directamente en el diseñador de flujo de trabajo o en el editor XML para trabajar con el archivo XAML.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-238">You can open directly in the Workflow designer or in the XML editor to work with the XAML.</span></span>
6. <span data-ttu-id="6f0e1-239">Agregue la siguiente lista de argumentos nuevos como elementos de línea separados en la pestaña de argumentos del diseñador de flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-239">Add the following list of new arguments as separate line items in the arguments tab of the workflow designer.</span></span> <span data-ttu-id="6f0e1-240">Todos los argumentos deben tener la dirección=In y el tipo=String.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-240">All arguments should have direction=In and type=String.</span></span> <span data-ttu-id="6f0e1-241">Estos se usarán para que los parámetros fluyan desde la definición de compilación hasta el flujo de trabajo, los cuales, posteriormente, se acostumbran a llamar al script de publicación.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-241">These will be used to flow parameters from the build definition into the workflow, which then get used to call the publish script.</span></span>

       SubscriptionName
       StorageAccountName
       CloudConfigLocation
       PackageLocation
       Environment
       SubscriptionDataFileLocation
       PublishScriptLocation
       ServiceName

   ![Lista de argumentos][3]

   <span data-ttu-id="6f0e1-243">El archivo XAML correspondiente se parece a este:</span><span class="sxs-lookup"><span data-stu-id="6f0e1-243">The corresponding XAML looks like this:</span></span>

       <Activity  _ />
         <x:Members>
           <x:Property Name="BuildSettings" Type="InArgument(mtbwa:BuildSettings)" />
           <x:Property Name="TestSpecs" Type="InArgument(mtbwa:TestSpecList)" />
           <x:Property Name="BuildNumberFormat" Type="InArgument(x:String)" />
           <x:Property Name="CleanWorkspace" Type="InArgument(mtbwa:CleanWorkspaceOption)" />
           <x:Property Name="RunCodeAnalysis" Type="InArgument(mtbwa:CodeAnalysisOption)" />
           <x:Property Name="SourceAndSymbolServerSettings" Type="InArgument(mtbwa:SourceAndSymbolServerSettings)" />
           <x:Property Name="AgentSettings" Type="InArgument(mtbwa:AgentSettings)" />
           <x:Property Name="AssociateChangesetsAndWorkItems" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateWorkItem" Type="InArgument(x:Boolean)" />
           <x:Property Name="DropBuild" Type="InArgument(x:Boolean)" />
           <x:Property Name="MSBuildArguments" Type="InArgument(x:String)" />
           <x:Property Name="MSBuildPlatform" Type="InArgument(mtbwa:ToolPlatform)" />
           <x:Property Name="PerformTestImpactAnalysis" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateLabel" Type="InArgument(x:Boolean)" />
           <x:Property Name="DisableTests" Type="InArgument(x:Boolean)" />
           <x:Property Name="GetVersion" Type="InArgument(x:String)" />
           <x:Property Name="PrivateDropLocation" Type="InArgument(x:String)" />
           <x:Property Name="Verbosity" Type="InArgument(mtbw:BuildVerbosity)" />
           <x:Property Name="Metadata" Type="mtbw:ProcessParameterMetadataCollection" />
           <x:Property Name="SupportedReasons" Type="mtbc:BuildReason" />
           <x:Property Name="SubscriptionName" Type="InArgument(x:String)" />
           <x:Property Name="StorageAccountName" Type="InArgument(x:String)" />
           <x:Property Name="CloudConfigLocation" Type="InArgument(x:String)" />
           <x:Property Name="PackageLocation" Type="InArgument(x:String)" />
           <x:Property Name="Environment" Type="InArgument(x:String)" />
           <x:Property Name="SubscriptionDataFileLocation" Type="InArgument(x:String)" />
           <x:Property Name="PublishScriptLocation" Type="InArgument(x:String)" />
           <x:Property Name="ServiceName" Type="InArgument(x:String)" />
         </x:Members>

         <this:Process.MSBuildArguments>
7. <span data-ttu-id="6f0e1-244">Agregue una secuencia nueva al final de Ejecutar en el agente:</span><span class="sxs-lookup"><span data-stu-id="6f0e1-244">Add a new sequence at the end of Run On Agent:</span></span>

   1. <span data-ttu-id="6f0e1-245">Comience agregando una actividad de instrucción If para verificar un archivo de script válido.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-245">Start by adding an If Statement activity to check for a valid script file.</span></span> <span data-ttu-id="6f0e1-246">Establezca la condición según este valor:</span><span class="sxs-lookup"><span data-stu-id="6f0e1-246">Set the condition to this value:</span></span>

          Not String.IsNullOrEmpty(PublishScriptLocation)
   2. <span data-ttu-id="6f0e1-247">En el caso Then de la instrucción If, agregue una actividad de secuencia nueva.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-247">In the Then case of the If Statement, add a new Sequence activity.</span></span> <span data-ttu-id="6f0e1-248">Establezca el nombre para mostrar en 'Iniciar publicación'</span><span class="sxs-lookup"><span data-stu-id="6f0e1-248">Set the display name to 'Start publish'</span></span>
   3. <span data-ttu-id="6f0e1-249">Con la secuencia Iniciar publicación todavía seleccionada, agregue la siguiente lista de variables nuevas como elementos de línea separados en la pestaña de variables del diseñador de flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-249">With the Start publish sequence still selected, add the following list of new variables as separate line items in the variables tab of the workflow designer.</span></span> <span data-ttu-id="6f0e1-250">Todas las variables deben tener el tipo de variable =Cadena y el ámbito =Iniciar publicación.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-250">All variables should have Variable type =String and Scope=Start publish.</span></span> <span data-ttu-id="6f0e1-251">Estos se usarán para que los parámetros fluyan desde la definición de compilación hasta el flujo de trabajo, los cuales, posteriormente, se acostumbran a llamar al script de publicación.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-251">These will be used to flow parameters from the build definition into the workflow, which then get used to call the publish script.</span></span>

      * <span data-ttu-id="6f0e1-252">SubscriptionDataFilePath, de tipo Cadena</span><span class="sxs-lookup"><span data-stu-id="6f0e1-252">SubscriptionDataFilePath, of type String</span></span>
      * <span data-ttu-id="6f0e1-253">PublishScriptFilePath, de tipo Cadena</span><span class="sxs-lookup"><span data-stu-id="6f0e1-253">PublishScriptFilePath, of type String</span></span>

        ![Nuevas variables][4]
   4. <span data-ttu-id="6f0e1-255">Si está utilizando TFS 2012 o anterior, agregue una actividad ConvertWorkspaceItem al comienzo de la nueva secuencia.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-255">If you are using TFS 2012 or earlier, add a ConvertWorkspaceItem activity at the beginning of the new Sequence.</span></span> <span data-ttu-id="6f0e1-256">Si está utilizando TFS 2013 o posterior, agregue una actividad GetLocalPath al comienzo de la nueva secuencia.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-256">If you are using TFS 2013 or later, add a GetLocalPath activity at the beginning of the new sequence.</span></span> <span data-ttu-id="6f0e1-257">En ConvertWorkspaceItem, establezca las propiedades de la manera siguiente: Direction=ServerToLocal, DisplayName='Convert publish script filename', Input=' PublishScriptLocation', Result='PublishScriptFilePath', Workspace='Workspace'.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-257">For a ConvertWorkspaceItem, set the properties as follows: Direction=ServerToLocal, DisplayName='Convert publish script filename', Input=' PublishScriptLocation', Result='PublishScriptFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="6f0e1-258">Para una actividad GetLocalPath, establezca la propiedad IncomingPath en 'PublishScriptLocation' y el resultado en 'PublishScriptFilePath'.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-258">For a GetLocalPath activity, set the property IncomingPath to 'PublishScriptLocation', and the Result to 'PublishScriptFilePath'.</span></span> <span data-ttu-id="6f0e1-259">Esta actividad convierte la ruta al script de publicación desde las ubicaciones del servidor TFS (si corresponde) hasta una ruta de disco local estándar.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-259">This activity converts the path to the publish script from TFS server locations (if applicable) to a standard local disk path.</span></span>
   5. <span data-ttu-id="6f0e1-260">Si está utilizando TFS 2012 o anterior, agregue otra actividad ConvertWorkspaceItem al final de la nueva secuencia.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-260">If you are using TFS 2012 or earlier, add another ConvertWorkspaceItem activity at the end of the new Sequence.</span></span> <span data-ttu-id="6f0e1-261">Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-261">Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="6f0e1-262">Si está utilizando TFS 2013 o posterior, agregue otro GetLocalPath.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-262">If you are using TFS 2013 or later, add another GetLocalPath.</span></span> <span data-ttu-id="6f0e1-263">IncomingPath='SubscriptionDataFileLocation' y Result='SubscriptionDataFilePath.'</span><span class="sxs-lookup"><span data-stu-id="6f0e1-263">IncomingPath='SubscriptionDataFileLocation', and Result='SubscriptionDataFilePath.'</span></span>
   6. <span data-ttu-id="6f0e1-264">Agregue una actividad InvokeProcess al final de la secuencia nueva.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-264">Add an InvokeProcess activity at the end of the new Sequence.</span></span>
      <span data-ttu-id="6f0e1-265">Esta actividad llama a PowerShell.exe con los argumentos pasados por la definición de compilación.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-265">This activity calls PowerShell.exe with the arguments passed in by the Build Definition.</span></span>

      + <span data-ttu-id="6f0e1-266">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span><span class="sxs-lookup"><span data-stu-id="6f0e1-266">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span></span>
      + <span data-ttu-id="6f0e1-267">DisplayName =Ejecutar script de publicación</span><span class="sxs-lookup"><span data-stu-id="6f0e1-267">DisplayName = Execute publish script</span></span>
      + <span data-ttu-id="6f0e1-268">FileName = "PowerShell" (incluir las comillas)</span><span class="sxs-lookup"><span data-stu-id="6f0e1-268">FileName = "PowerShell" (include the quotes)</span></span>
      + <span data-ttu-id="6f0e1-269">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span><span class="sxs-lookup"><span data-stu-id="6f0e1-269">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span></span>
   7. <span data-ttu-id="6f0e1-270">En el cuadro de texto de la sección **Controlar salida estándar** de InvokeProcess, establezca el valor del cuadro de texto en 'data'.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-270">In the **Handle Standard Output** section textbox of the InvokeProcess, set the textbox value to 'data'.</span></span> <span data-ttu-id="6f0e1-271">Esta es una variable para almacenar los datos de salida estándar.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-271">This is a variable to store the standard output data.</span></span>
   8. <span data-ttu-id="6f0e1-272">Agregue una actividad WriteBuildMessage justo debajo de la sección **Controlar salida estándar** .</span><span class="sxs-lookup"><span data-stu-id="6f0e1-272">Add a WriteBuildMessage activity just below the **Handle Standard Output** section.</span></span> <span data-ttu-id="6f0e1-273">Establezca la importancia = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' y el mensaje ='data'.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-273">Set the Importance = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' and the Message='data'.</span></span> <span data-ttu-id="6f0e1-274">Esto asegura que la salida estándar del script se escriba en la salida de la compilación.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-274">This ensures the standard output of the script will get written to the build output.</span></span>
   9. <span data-ttu-id="6f0e1-275">En el cuadro de texto de la sección **Controlar salida de errores** de InvokeProcess, establezca el valor del cuadro de texto en 'data'.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-275">In the **Handle Error Output** section textbox of the InvokeProcess, set the textbox value to 'data'.</span></span> <span data-ttu-id="6f0e1-276">Esta es una variable para almacenar los datos de error estándar.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-276">This is a variable to store the standard error data.</span></span>
   10. <span data-ttu-id="6f0e1-277">Agregue una actividad WriteBuildError justo debajo de la sección **Controlar salida de errores** .</span><span class="sxs-lookup"><span data-stu-id="6f0e1-277">Add a WriteBuildError activity just below the **Handle Error Output** section.</span></span> <span data-ttu-id="6f0e1-278">Establezca el mensaje='data'.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-278">Set the Message='data'.</span></span> <span data-ttu-id="6f0e1-279">Esto asegura que los errores estándar del script se escriban en la salida de error de compilación.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-279">This ensures the standard errors of the script will get written to the build error output.</span></span>
   11. <span data-ttu-id="6f0e1-280">Corrija los errores, que se indican por signos de exclamación azules.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-280">Correct any errors, indicated by blue exclamation marks.</span></span> <span data-ttu-id="6f0e1-281">Mueva el puntero sobre los signos de exclamación para obtener una sugerencia del error.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-281">Hover over the exclamation marks to get a hint about the error.</span></span> <span data-ttu-id="6f0e1-282">Guarde el flujo de trabajo para borrar errores.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-282">Save the workflow to clear errors.</span></span>

   <span data-ttu-id="6f0e1-283">El resultado final de las actividades de flujo de trabajo de publicación se verán en el diseñador de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="6f0e1-283">The final result of the publish workflow activities will look like this in the designer:</span></span>

   ![Actividades de flujo de trabajo][5]

   <span data-ttu-id="6f0e1-285">El resultado final de las actividades de flujo de trabajo de publicación se verán en el archivo XAML de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="6f0e1-285">The final result of the publish workflow activities will look like this in XAML:</span></span>

       <If Condition="[Not String.IsNullOrEmpty(PublishScriptLocation)]" sap2010:WorkflowViewState.IdRef="If_1">
           <If.Then>
             <Sequence DisplayName="Start Publish" sap2010:WorkflowViewState.IdRef="Sequence_4">
               <Sequence.Variables>
                 <Variable x:TypeArguments="x:String" Name="SubscriptionDataFilePath" />
                 <Variable x:TypeArguments="x:String" Name="PublishScriptFilePath" />
               </Sequence.Variables>
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert publish script filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_1" Input="[PublishScriptLocation]" Result="[PublishScriptFilePath]" Workspace="[Workspace]" />
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert subscription filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_2" Input="[SubscriptionDataFileLocation]" Result="[SubscriptionDataFilePath]" Workspace="[Workspace]" />
               <mtbwa:InvokeProcess Arguments="[String.Format(&quot; -File &quot;&quot;{0}&quot;&quot; -serviceName {1}&#xD;&#xA;            -storageAccountName {2} -packageLocation &quot;&quot;{3}&quot;&quot;&#xD;&#xA;            -cloudConfigLocation &quot;&quot;{4}&quot;&quot; -subscriptionDataFile &quot;&quot;{5}&quot;&quot;&#xD;&#xA;            -selectedSubscription {6} -environment &quot;&quot;{7}&quot;&quot;&quot;,&#xD;&#xA;            PublishScriptFilePath, ServiceName, StorageAccountName,&#xD;&#xA;            PackageLocation, CloudConfigLocation,&#xD;&#xA;            SubscriptionDataFilePath, SubscriptionName, Environment)]" DisplayName="'Execute Publish Script'" FileName="[PowerShell]" sap2010:WorkflowViewState.IdRef="InvokeProcess_1">
                 <mtbwa:InvokeProcess.ErrorDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildError Message="{x:Null}" sap2010:WorkflowViewState.IdRef="WriteBuildError_1" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.ErrorDataReceived>
                 <mtbwa:InvokeProcess.OutputDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildMessage sap2010:WorkflowViewState.IdRef="WriteBuildMessage_2" Importance="[Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High]" Message="[data]" mva:VisualBasic.Settings="Assembly references and imported namespaces serialized as XML namespaces" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.OutputDataReceived>
               </mtbwa:InvokeProcess>
             </Sequence>
           </If.Then>
         </If>
       </Sequence>
8. <span data-ttu-id="6f0e1-286">Guarde el flujo de trabajo de la plantilla del proceso de compilación y proteja este archivo.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-286">Save the build process template workflow and Check In this file.</span></span>
9. <span data-ttu-id="6f0e1-287">Edite la definición de compilación (ciérrela si estuviera abierta) y seleccione el botón **Nuevo** si todavía no ve la nueva plantilla en la lista de plantillas del proceso.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-287">Edit the build definition (close it if it is already open), and select the **New** button if you do not yet see the new template in the list of Process Templates.</span></span>
10. <span data-ttu-id="6f0e1-288">Establezca los valores de propiedad del parámetro en la sección Misc como a continuación:</span><span class="sxs-lookup"><span data-stu-id="6f0e1-288">Set the parameter property values in the Misc section as follows:</span></span>

    1. <span data-ttu-id="6f0e1-289">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *Este valor se obtiene de: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span><span class="sxs-lookup"><span data-stu-id="6f0e1-289">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *This value is derived from: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span></span>
    2. <span data-ttu-id="6f0e1-290">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *Este valor se obtiene de:($PublishDir)($ProjectName).cspkg*</span><span class="sxs-lookup"><span data-stu-id="6f0e1-290">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *This value is derived from: ($PublishDir)($ProjectName).cspkg*</span></span>
    3. <span data-ttu-id="6f0e1-291">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span><span class="sxs-lookup"><span data-stu-id="6f0e1-291">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span></span>
    4. <span data-ttu-id="6f0e1-292">ServiceName = 'mycloudservicename' *Use el nombre de servicio en la nube adecuado aquí*</span><span class="sxs-lookup"><span data-stu-id="6f0e1-292">ServiceName = 'mycloudservicename' *Use the appropriate cloud service name here*</span></span>
    5. <span data-ttu-id="6f0e1-293">Entorno = 'Staging'</span><span class="sxs-lookup"><span data-stu-id="6f0e1-293">Environment = 'Staging'</span></span>
    6. <span data-ttu-id="6f0e1-294">StorageAccountName = 'mystorageaccountname' *Use el nombre de cuenta de almacenamiento adecuado aquí*</span><span class="sxs-lookup"><span data-stu-id="6f0e1-294">StorageAccountName = 'mystorageaccountname' *Use the appropriate storage account name here*</span></span>
    7. <span data-ttu-id="6f0e1-295">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span><span class="sxs-lookup"><span data-stu-id="6f0e1-295">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span></span>
    8. <span data-ttu-id="6f0e1-296">SubscriptionName = 'default'</span><span class="sxs-lookup"><span data-stu-id="6f0e1-296">SubscriptionName = 'default'</span></span>

    ![Valores de propiedad de parámetro][6]
11. <span data-ttu-id="6f0e1-298">Guarde los cambios en la Definición de compilación.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-298">Save the changes to the Build Definition.</span></span>
12. <span data-ttu-id="6f0e1-299">Ponga una compilación en cola para ejecutar la compilación del paquete y la publicación.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-299">Queue a Build to execute both the package build and publish.</span></span> <span data-ttu-id="6f0e1-300">Si tiene un desencadenador establecido en Integración continua, ejecutará este comportamiento en cada protección.</span><span class="sxs-lookup"><span data-stu-id="6f0e1-300">If you have a trigger set to Continuous Integration, you will execute this behavior on every check-in.</span></span>

### <a name="publishcloudserviceps1-script-template"></a><span data-ttu-id="6f0e1-301">Plantilla de script PublishCloudService.ps1</span><span class="sxs-lookup"><span data-stu-id="6f0e1-301">PublishCloudService.ps1 script template</span></span>
```
Param(  $serviceName = "",
        $storageAccountName = "",
        $packageLocation = "",
        $cloudConfigLocation = "",
        $environment = "Staging",
        $deploymentLabel = "ContinuousDeploy to $servicename",
        $timeStampFormat = "g",
        $alwaysDeleteExistingDeployments = 1,
        $enableDeploymentUpgrade = 1,
        $selectedsubscription = "default",
        $subscriptionDataFile = ""
     )


function Publish()
{
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot -ErrorVariable a -ErrorAction silentlycontinue
    if ($a[0] -ne $null)
    {
        Write-Output "$(Get-Date -f $timeStampFormat) - No deployment is detected. Creating a new deployment. "
    }
    #check for existing deployment and then either upgrade, delete + deploy, or cancel according to $alwaysDeleteExistingDeployments and $enableDeploymentUpgrade boolean variables
    if ($deployment.Name -ne $null)
    {
        switch ($alwaysDeleteExistingDeployments)
        {
            1
            {
                switch ($enableDeploymentUpgrade)
                {
                    1  #Update deployment inplace (usually faster, cheaper, won't destroy VIP)
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Upgrading deployment."
                        UpgradeDeployment
                    }
                    0  #Delete then create new deployment
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Deleting deployment."
                        DeleteDeployment
                        CreateNewDeployment

                    }
                } # switch ($enableDeploymentUpgrade)
            }
            0
            {
                Write-Output "$(Get-Date -f $timeStampFormat) - ERROR: Deployment exists in $servicename.  Script execution cancelled."
                exit
            }
        } #switch ($alwaysDeleteExistingDeployments)
    } else {
            CreateNewDeployment
    }
}

function CreateNewDeployment()
{
    write-progress -id 3 -activity "Creating New Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: In progress"

    $opstat = New-AzureDeployment -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Creating New Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: Complete, Deployment ID: $completeDeploymentID"

    StartInstances
}

function UpgradeDeployment()
{
    write-progress -id 3 -activity "Upgrading Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: In progress"

    # perform Update-Deployment
    $setdeployment = Set-AzureDeployment -Upgrade -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName -Force

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Upgrading Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: Complete, Deployment ID: $completeDeploymentID"
}

function DeleteDeployment()
{

    write-progress -id 2 -activity "Deleting Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: In progress"

    #WARNING - always deletes with force
    $removeDeployment = Remove-AzureDeployment -Slot $slot -ServiceName $serviceName -Force

    write-progress -id 2 -activity "Deleting Deployment: Complete" -completed -Status $removeDeployment
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: Complete"

}

function StartInstances()
{
    write-progress -id 4 -activity "Starting Instances" -status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: In progress"

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $runstatus = $deployment.Status

    if ($runstatus -ne 'Running')
    {
        $run = Set-AzureDeployment -Slot $slot -ServiceName $serviceName -Status Running
    }
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $oldStatusStr = @("") * $deployment.RoleInstanceList.Count

    while (-not(AllInstancesRunning($deployment.RoleInstanceList)))
    {
        $i = 1
        foreach ($roleInstance in $deployment.RoleInstanceList)
        {
            $instanceName = $roleInstance.InstanceName
            $instanceStatus = $roleInstance.InstanceStatus

            if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
            {
                $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
                Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
            }

            write-progress -id (4 + $i) -activity "Starting Instance '$instanceName'" -status "$instanceStatus"
            $i = $i + 1
        }

        sleep -Seconds 1

        $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    }

    $i = 1
    foreach ($roleInstance in $deployment.RoleInstanceList)
    {
        $instanceName = $roleInstance.InstanceName
        $instanceStatus = $roleInstance.InstanceStatus

        if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
        {
            $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
            Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
        }

        $i = $i + 1
    }

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $opstat = $deployment.Status

    write-progress -id 4 -activity "Starting Instances" -completed -status $opstat
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: $opstat"
}

function AllInstancesRunning($roleInstanceList)
{
    foreach ($roleInstance in $roleInstanceList)
    {
        if ($roleInstance.InstanceStatus -ne "ReadyRole")
        {
            return $false
        }
    }

    return $true
}

#configure powershell with Azure 1.7 modules
Import-Module Azure

#configure powershell with publishsettings for your subscription
$pubsettings = $subscriptionDataFile
Import-AzurePublishSettingsFile $pubsettings
Set-AzureSubscription -CurrentStorageAccountName $storageAccountName -SubscriptionName $selectedsubscription
Select-AzureSubscription $selectedsubscription

#set remaining environment variables for Azure cmdlets
$subscription = Get-AzureSubscription $selectedsubscription
$subscriptionname = $subscription.subscriptionname
$subscriptionid = $subscription.subscriptionid
$slot = $environment

#main driver - publish & write progress to activity log
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script started."
Write-Output "$(Get-Date -f $timeStampFormat) - Preparing deployment of $deploymentLabel for $subscriptionname with Subscription ID $subscriptionid."

Publish

$deployment = Get-AzureDeployment -slot $slot -serviceName $servicename
$deploymentUrl = $deployment.Url

Write-Output "$(Get-Date -f $timeStampFormat) - Created Cloud Service with URL $deploymentUrl."
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script finished."
```

## <a name="next-steps"></a><span data-ttu-id="6f0e1-302">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6f0e1-302">Next steps</span></span>
<span data-ttu-id="6f0e1-303">Para habilitar la depuración remota cuando se usa la entrega continua, consulte [Habilitación de la depuración remota al usar la entrega continua para publicar en Azure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span><span class="sxs-lookup"><span data-stu-id="6f0e1-303">To enable remote debugging when using continuous delivery, see [Enable remote debugging when using continuous delivery to publish to Azure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span></span>

[Team Foundation Build Service]: https://msdn.microsoft.com/library/ee259687.aspx
[.NET Framework 4]: https://www.microsoft.com/download/details.aspx?id=17851
[.NET Framework 4.5]: https://www.microsoft.com/download/details.aspx?id=30653
[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42643
[Scale out your build system]: https://msdn.microsoft.com/library/dd793166.aspx
[Deploy and configure a build server]: https://msdn.microsoft.com/library/ms181712.aspx
[Azure PowerShell cmdlets]: /powershell/azureps-cmdlets-docs
[the .publishsettings file]: https://manage.windowsazure.com/download/publishprofile.aspx?wa=wsignin1.0
[0]: ./media/cloud-services-dotnet-continuous-delivery/tfs-01bc.png
[2]: ./media/cloud-services-dotnet-continuous-delivery/tfs-02.png
[3]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-03.png
[4]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-04.png
[5]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-05.png
[6]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-06.png
