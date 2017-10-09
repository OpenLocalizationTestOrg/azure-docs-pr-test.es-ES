---
title: Servicios de entrega de aaaContinuous para la nube con TFS en Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo las aplicaciones de nube tooset la entrega continua de Azure. Ejemplos de código para las instrucciones de línea de comandos de MSBuild y scripts PowerShell."
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
ms.openlocfilehash: c0e5e72ffbd3c05b84ce1733068e92c528bcc4b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-for-cloud-services-in-azure"></a><span data-ttu-id="d3f68-104">Entrega continua para Servicios en la nube de Azure</span><span class="sxs-lookup"><span data-stu-id="d3f68-104">Continuous Delivery for Cloud Services in Azure</span></span>
<span data-ttu-id="d3f68-105">Hello proceso descrito en este artículo muestra cómo tooset la entrega continua para aplicaciones de nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="d3f68-105">hello process described in this article shows you how tooset up continuous delivery for Azure cloud apps.</span></span> <span data-ttu-id="d3f68-106">Este proceso le permite crear automáticamente paquetes e implementar Hola paquete tooAzure después de cada comprobación de código.</span><span class="sxs-lookup"><span data-stu-id="d3f68-106">This process enables you to automatically create packages and deploy hello package tooAzure after every code check-in.</span></span> <span data-ttu-id="d3f68-107">proceso de compilación del paquete se describe en este artículo Hello es equivalente toohello **paquete** comandos en Visual Studio y los pasos de publicación son equivalente toohello **publicar** en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3f68-107">hello package build process described in this article is equivalent toohello **Package** command in Visual Studio, and the publishing steps are equivalent toohello **Publish** command in Visual Studio.</span></span>
<span data-ttu-id="d3f68-108">Hola artículo abarca Hola métodos que usaría toocreate un servidor de compilación con instrucciones de línea de comandos de MSBuild y scripts de Windows PowerShell y también se muestra cómo toooptionally configurar Visual Studio Team Foundation Server - definiciones de Team Build comandos de MSBuild hello toouse y scripts de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d3f68-108">hello article covers hello methods you would use toocreate a build server with MSBuild command-line statements and Windows PowerShell scripts, and it also demonstrates how toooptionally configure Visual Studio Team Foundation Server - Team Build definitions toouse hello MSBuild commands and PowerShell scripts.</span></span> <span data-ttu-id="d3f68-109">proceso de Hello es personalizable para su entorno de compilación y los entornos de destino de Azure.</span><span class="sxs-lookup"><span data-stu-id="d3f68-109">hello process is customizable for your build environment and Azure target environments.</span></span>

<span data-ttu-id="d3f68-110">También puede usar Visual Studio Team Services, una versión de TFS que está hospedado en Azure, toodo esto más fácilmente.</span><span class="sxs-lookup"><span data-stu-id="d3f68-110">You can also use Visual Studio Team Services, a version of TFS that is hosted in Azure, toodo this more easily.</span></span> 

<span data-ttu-id="d3f68-111">Antes de comenzar, debe publicar su aplicación desde Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3f68-111">Before you start, you should publish your application from Visual Studio.</span></span>
<span data-ttu-id="d3f68-112">Así se asegurará de que todos los recursos de hello están disponibles y se inicializa al intentar el proceso de publicación de tooautomate Hola.</span><span class="sxs-lookup"><span data-stu-id="d3f68-112">This will ensure that all hello resources are available and initialized when you attempt tooautomate hello publication process.</span></span>

## <a name="1-configure-hello-build-server"></a><span data-ttu-id="d3f68-113">1: configurar Hola Build Server</span><span class="sxs-lookup"><span data-stu-id="d3f68-113">1: Configure hello Build Server</span></span>
<span data-ttu-id="d3f68-114">Para poder crear un paquete de Azure mediante el uso de MSBuild, debe instalar Hola requerido software y las herramientas en el servidor de compilación Hola.</span><span class="sxs-lookup"><span data-stu-id="d3f68-114">Before you can create an Azure package by using MSBuild, you must install hello required software and tools on hello build server.</span></span>

<span data-ttu-id="d3f68-115">Visual Studio no es necesario toobe instalado en el servidor de compilación Hola.</span><span class="sxs-lookup"><span data-stu-id="d3f68-115">Visual Studio is not required toobe installed on hello build server.</span></span> <span data-ttu-id="d3f68-116">Si desea que el servidor de compilación toouse toomanage de servicio de Team Foundation Build, siga las instrucciones de Hola Hola [servicio de Team Foundation Build] [ Team Foundation Build Service] documentación.</span><span class="sxs-lookup"><span data-stu-id="d3f68-116">If you want toouse Team Foundation Build Service toomanage your build server, follow hello instructions in hello [Team Foundation Build Service][Team Foundation Build Service] documentation.</span></span>

1. <span data-ttu-id="d3f68-117">En el servidor de compilación de hello, instale hello [.NET Framework 4.5.2][.NET Framework 4.5.2], que incluye MSBuild.</span><span class="sxs-lookup"><span data-stu-id="d3f68-117">On hello build server, install hello [.NET Framework 4.5.2][.NET Framework 4.5.2], which includes MSBuild.</span></span>
2. <span data-ttu-id="d3f68-118">Instalar más reciente hello [herramientas de creación de Azure para .NET](https://azure.microsoft.com/develop/net/).</span><span class="sxs-lookup"><span data-stu-id="d3f68-118">Install hello latest [Azure Authoring Tools for .NET](https://azure.microsoft.com/develop/net/).</span></span>
3. <span data-ttu-id="d3f68-119">Instalar hello [bibliotecas de Azure para .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span><span class="sxs-lookup"><span data-stu-id="d3f68-119">Install hello [Azure Libraries for .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span></span>
4. <span data-ttu-id="d3f68-120">Servidor de compilación del archivo de copia hello Microsoft.WebApplication.targets de una toohello de instalación de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3f68-120">Copy hello Microsoft.WebApplication.targets file from a Visual Studio installation toohello build server.</span></span>

   <span data-ttu-id="d3f68-121">En un equipo con Visual Studio instalado, este archivo se encuentra en el directorio de hello C:\\Program Files(x86)%\\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications.</span><span class="sxs-lookup"><span data-stu-id="d3f68-121">On a computer with Visual Studio installed, this file is located in hello directory C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications.</span></span> <span data-ttu-id="d3f68-122">Debe copiar toohello mismo directorio en el servidor de compilación Hola.</span><span class="sxs-lookup"><span data-stu-id="d3f68-122">You should copy it toohello same directory on hello build server.</span></span>
5. <span data-ttu-id="d3f68-123">Instalar hello [Azure Tools para Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="d3f68-123">Install hello [Azure Tools for Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span></span>

## <a name="2-build-a-package-using-msbuild-commands"></a><span data-ttu-id="d3f68-124">2 Compilación de un paquete con comandos de MSBuild</span><span class="sxs-lookup"><span data-stu-id="d3f68-124">2: Build a Package using MSBuild Commands</span></span>
<span data-ttu-id="d3f68-125">Esta sección describe cómo tooconstruct un MSBuild comando que crea un paquete de Azure.</span><span class="sxs-lookup"><span data-stu-id="d3f68-125">This section describes how tooconstruct an MSBuild command that builds an Azure package.</span></span> <span data-ttu-id="d3f68-126">Ejecutar este paso en tooverify de servidor de compilación de Hola que todo está configurado correctamente y encargada de comandos de MSBuild Hola lo que le gustaría toodo.</span><span class="sxs-lookup"><span data-stu-id="d3f68-126">Run this step on hello build server tooverify that everything is configured correctly and that hello MSBuild command does what you want it toodo.</span></span> <span data-ttu-id="d3f68-127">Puede agregar esta tooexisting de línea de comandos generar secuencias de comandos en el servidor de compilación de hello, o puede usar la línea de comandos de hello en una definición de compilación de TFS, tal y como se describe en la sección siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="d3f68-127">You can either add this command line tooexisting build scripts on hello build server, or you can use hello command line in a TFS Build Definition, as described in hello next section.</span></span> <span data-ttu-id="d3f68-128">Para obtener más información acerca de los parámetros de línea de comandos y MSBuild, consulte [Referencia de la línea de comandos de MSBuild](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="d3f68-128">For more information about command-line parameters and MSBuild, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>

1. <span data-ttu-id="d3f68-129">Si Visual Studio está instalado en el servidor de compilación de hello, busque y seleccione **Visual Studio Command Prompt** en hello **Visual Studio Tools** carpeta de Windows.</span><span class="sxs-lookup"><span data-stu-id="d3f68-129">If Visual Studio is installed on hello build server, locate and choose **Visual Studio Command Prompt** in hello **Visual Studio Tools** folder in Windows.</span></span>

   <span data-ttu-id="d3f68-130">Si Visual Studio no está instalado en el servidor de compilación de hello, abra un símbolo del sistema y asegúrese de que MSBuild.exe es accesible en la ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="d3f68-130">If Visual Studio is not installed on hello build server, open a command prompt and make sure that MSBuild.exe is accessible on the path.</span></span> <span data-ttu-id="d3f68-131">MSBuild se instala con .NET Framework de hello en hello ruta de acceso % WINDIR %\\Microsoft.NET\\Framework\\*versión*.</span><span class="sxs-lookup"><span data-stu-id="d3f68-131">MSBuild is installed with hello .NET Framework in hello path %WINDIR%\\Microsoft.NET\\Framework\\*Version*.</span></span> <span data-ttu-id="d3f68-132">Por ejemplo, para agregar la variable de entorno PATH de MSBuild.exe toohello si tiene instalado .NET Framework 4, escriba Hola siguiente comando en el símbolo del sistema de hello:</span><span class="sxs-lookup"><span data-stu-id="d3f68-132">For example, to add MSBuild.exe toohello PATH environment variable when you have .NET Framework 4 installed, type hello following command at hello command prompt:</span></span>

       set PATH=%PATH%;"C:\Windows\Microsoft.NET\Framework\v4.0.30319"
2. <span data-ttu-id="d3f68-133">En el símbolo de hello, desplazarse por las carpetas de toohello que contiene el archivo de proyecto de Azure que desea toobuild.</span><span class="sxs-lookup"><span data-stu-id="d3f68-133">At hello command prompt, navigate toohello folder containing the Azure project file that you want toobuild.</span></span>
3. <span data-ttu-id="d3f68-134">Ejecute MSBuild con/target hello: opción como en el siguiente ejemplo de Hola de publicación:</span><span class="sxs-lookup"><span data-stu-id="d3f68-134">Run MSBuild with hello /target:Publish option as in hello following example:</span></span>

       MSBuild /target:Publish

   <span data-ttu-id="d3f68-135">Esta opción se puede abreviar como /t:Publish.</span><span class="sxs-lookup"><span data-stu-id="d3f68-135">This option can be abbreviated as /t:Publish.</span></span> <span data-ttu-id="d3f68-136">opción de /t:Publish Hello en MSBuild no debe confundirse con los comandos de publicación de hello disponibles en Visual Studio cuando tienes hello que Azure SDK instalado.</span><span class="sxs-lookup"><span data-stu-id="d3f68-136">hello /t:Publish option in MSBuild should not be confused with hello Publish commands available in Visual Studio when you have hello Azure SDK installed.</span></span> <span data-ttu-id="d3f68-137">Hola /t: opción de publicación solo compilaciones Hola paquetes de Azure.</span><span class="sxs-lookup"><span data-stu-id="d3f68-137">hello /t:Publish option only builds hello Azure packages.</span></span> <span data-ttu-id="d3f68-138">No implementa paquetes de saludo como Hola publicar comandos en Visual Studio tienen.</span><span class="sxs-lookup"><span data-stu-id="d3f68-138">It does not deploy hello packages as hello Publish commands in Visual Studio do.</span></span>

   <span data-ttu-id="d3f68-139">Si lo desea, puede especificar el nombre del proyecto de Hola como un parámetro de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="d3f68-139">Optionally, you can specify hello project name as an MSBuild parameter.</span></span> <span data-ttu-id="d3f68-140">Si no se especifica, se utiliza el directorio actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3f68-140">If not specified, hello current directory is used.</span></span> <span data-ttu-id="d3f68-141">Para más información acerca de las opciones de línea de comandos de MSBuild, consulte [Referencia de la línea de comandos de MSBuild1](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="d3f68-141">For more information about MSBuild command line options, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>
4. <span data-ttu-id="d3f68-142">Busque la salida de hello.</span><span class="sxs-lookup"><span data-stu-id="d3f68-142">Locate hello output.</span></span> <span data-ttu-id="d3f68-143">De forma predeterminada, este comando crea un directorio en carpeta de raíz de toohello de relación para el proyecto de hello, como *ProjectDir*\\bin\\*configuración* \\ App.Publish\\.</span><span class="sxs-lookup"><span data-stu-id="d3f68-143">By default, this command creates a directory in relation toohello root folder for hello project, such as *ProjectDir*\\bin\\*Configuration*\\app.publish\\.</span></span> <span data-ttu-id="d3f68-144">Al compilar un proyecto de Azure, se generan dos archivos, el propio archivo de paquete Hola y Hola que acompaña a archivo de configuración:</span><span class="sxs-lookup"><span data-stu-id="d3f68-144">When you build an Azure project, you generate two files, hello package file itself and hello accompanying configuration file:</span></span>

   * <span data-ttu-id="d3f68-145">Project.cspkg</span><span class="sxs-lookup"><span data-stu-id="d3f68-145">Project.cspkg</span></span>
   * <span data-ttu-id="d3f68-146">ServiceConfiguration.*TargetProfile*.cscfg</span><span class="sxs-lookup"><span data-stu-id="d3f68-146">ServiceConfiguration.*TargetProfile*.cscfg</span></span>

   <span data-ttu-id="d3f68-147">De manera predeterminada, cada proyecto de Azure incluye un archivo de configuración del servicio (archivo .cscfg) para las compilaciones locales (depuración) y otro para las compilaciones en la nube (ensayo o producción), pero puede agregar o quitar archivos de configuración del servicio según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="d3f68-147">By default, each Azure project includes one service configuration file (.cscfg file) for local (debugging) builds and another for cloud (staging or production) builds, but you can add or remove service configuration files as needed.</span></span> <span data-ttu-id="d3f68-148">Al compilar un paquete de Visual Studio, se le pedirá que tooinclude de archivo de configuración de servicio junto con el paquete de saludo.</span><span class="sxs-lookup"><span data-stu-id="d3f68-148">When you build a package within Visual Studio, you will be asked which service configuration file tooinclude alongside hello package.</span></span>
5. <span data-ttu-id="d3f68-149">Especifique el archivo de configuración de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3f68-149">Specify hello service configuration file.</span></span> <span data-ttu-id="d3f68-150">Al compilar un paquete con MSBuild, archivo de configuración de servicio local de Hola se incluye de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="d3f68-150">When you build a package by using MSBuild, hello local service configuration file is included by default.</span></span> <span data-ttu-id="d3f68-151">tooinclude un archivo de configuración de servicio diferente, establezca la propiedad de TargetProfile de comandos de MSBuild hello, como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="d3f68-151">tooinclude a different service configuration file, set the TargetProfile property of hello MSBuild command, as in hello following example:</span></span>

       MSBuild /t:Publish /p:TargetProfile=Cloud
6. <span data-ttu-id="d3f68-152">Especifique la ubicación de hello para la salida de hello.</span><span class="sxs-lookup"><span data-stu-id="d3f68-152">Specify hello location for hello output.</span></span> <span data-ttu-id="d3f68-153">Ruta de acceso del conjunto Hola utilizando el/p: PublishDir =*directorio* \\ opción, incluidos los Hola separador de barra diagonal inversa, como en el siguiente ejemplo de Hola final:</span><span class="sxs-lookup"><span data-stu-id="d3f68-153">Set hello path by using the /p:PublishDir=*Directory*\\ option, including hello trailing backslash separator, as in hello following example:</span></span>

       MSBuild /target:Publish /p:PublishDir=\\myserver\drops\

   <span data-ttu-id="d3f68-154">Una vez que haya construido y probar un MSBuild adecuado toobuild de línea de comandos de los proyectos y combinarlos en un paquete de Azure, puede agregar esta línea de comandos tooyour los scripts de compilación.</span><span class="sxs-lookup"><span data-stu-id="d3f68-154">Once you've constructed and tested an appropriate MSBuild command line toobuild your projects and combine them into an Azure package, you can add this command line tooyour build scripts.</span></span> <span data-ttu-id="d3f68-155">Si su servidor de compilación usa scripts personalizados, este proceso dependerá de los detalles de su proceso personalizado de compilación.</span><span class="sxs-lookup"><span data-stu-id="d3f68-155">If your build server uses custom scripts, this process will depend on the specifics of your custom build process.</span></span> <span data-ttu-id="d3f68-156">Si usa TFS como un entorno de compilación, a continuación, puede seguir las instrucciones de Hola Hola siguiente paso tooadd hello Azure paquete compilación tooyour proceso de compilación.</span><span class="sxs-lookup"><span data-stu-id="d3f68-156">If you are using TFS as a build environment, then you can follow hello instructions in hello next step tooadd hello Azure package build tooyour build process.</span></span>

## <a name="3-build-a-package-using-tfs-team-build"></a><span data-ttu-id="d3f68-157">3: Compilación de un paquete con TFS Team Build</span><span class="sxs-lookup"><span data-stu-id="d3f68-157">3: Build a Package using TFS Team Build</span></span>
<span data-ttu-id="d3f68-158">Si tiene configurado como servidor de compilación de un controlador de compilación y Hola Team Foundation Server (TFS) configurado como una máquina de compilación TFS, a continuación, opcionalmente, puede configurar una compilación automatizada para el paquete de Azure.</span><span class="sxs-lookup"><span data-stu-id="d3f68-158">If you have Team Foundation Server (TFS) set up as a build controller and hello build server set up as a TFS build machine, then you can optionally set up an automated build for your Azure package.</span></span> <span data-ttu-id="d3f68-159">Para obtener información sobre cómo tooset una y usar Team Foundation server como un sistema de compilación, consulte [escalar horizontalmente un sistema de compilación][Scale out your build system].</span><span class="sxs-lookup"><span data-stu-id="d3f68-159">For information on how tooset up and use Team Foundation server as a build system, see [Scale out your build system][Scale out your build system].</span></span> <span data-ttu-id="d3f68-160">En concreto, el siguiente procedimiento se supone que ha configurado el servidor de compilación tal y como se describe en [implementar y configurar un servidor de compilación][Deploy and configure a build server], y que ha creado un proyecto de equipo creado una nube proyecto de servicio en el proyecto de equipo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3f68-160">In particular, the following procedure assumes that you have configured your build server as described in [Deploy and configure a build server][Deploy and configure a build server], and that you have created a team project, created a cloud service project in hello team project.</span></span>

<span data-ttu-id="d3f68-161">tooconfigure TFS toobuild Azure realizado por paquetes, Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="d3f68-161">tooconfigure TFS toobuild Azure packages, perform hello following steps:</span></span>

1. <span data-ttu-id="d3f68-162">En Visual Studio en el equipo de desarrollo, en el menú de vista de hello, elija **Team Explorer**, o elija Ctrl +\\, Ctrl + M.</span><span class="sxs-lookup"><span data-stu-id="d3f68-162">In Visual Studio on your development computer, on hello View menu, choose **Team Explorer**, or choose Ctrl+\\, Ctrl+M.</span></span> <span data-ttu-id="d3f68-163">En la ventana de Team Explorer, expanda hello **compilaciones** nodo o elija hello **compilaciones** página y elija **nueva definición de compilación**.</span><span class="sxs-lookup"><span data-stu-id="d3f68-163">In the Team Explorer window, expand hello **Builds** node or choose hello **Builds** page, and choose **New Build Definition**.</span></span>

   ![Opción Nueva definición de compilación][0]
2. <span data-ttu-id="d3f68-165">Elija hello **desencadenador** pestaña y especificar Hola deseada condiciones para cuando desee Hola toobe paquete creado.</span><span class="sxs-lookup"><span data-stu-id="d3f68-165">Choose hello **Trigger** tab, and specify hello desired conditions for when you want hello package toobe built.</span></span> <span data-ttu-id="d3f68-166">Por ejemplo, especificar **integración continua** paquete de hello toobuild siempre que sea un origen de control en el repositorio se produce.</span><span class="sxs-lookup"><span data-stu-id="d3f68-166">For example, specify **Continuous Integration** toobuild hello package whenever a source control check-in occurs.</span></span>
3. <span data-ttu-id="d3f68-167">Elija hello **configuración del origen de** y a asegurarse de que la carpeta del proyecto aparece en hello **carpeta de Control de código fuente** columna, y el estado de hello es **Active**.</span><span class="sxs-lookup"><span data-stu-id="d3f68-167">Choose hello **Source Settings** tab, and make sure your project folder is listed in hello **Source Control Folder** column, and hello status is **Active**.</span></span>
4. <span data-ttu-id="d3f68-168">Elija hello **valores predeterminados de compilación** pestaña y en el controlador de compilación, compruebe el nombre de hello del servidor de compilación de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3f68-168">Choose hello **Build Defaults** tab, and under Build controller, verify hello name of hello build server.</span></span>  <span data-ttu-id="d3f68-169">Además, elija la opción hello **siguiente de toohello de salida de compilación copia la carpeta de entrega** y especifique la ubicación de destino de hello deseado.</span><span class="sxs-lookup"><span data-stu-id="d3f68-169">Also, choose hello option **Copy build output toohello following drop folder** and specify hello desired drop location.</span></span>
5. <span data-ttu-id="d3f68-170">Elija hello **proceso** ficha. En la ficha proceso de hello, elija plantilla predeterminada de hello, en **generar**, elija el proyecto de hello si aún no está seleccionado y expanda hello **avanzadas** sección Hola **compilar**sección de la cuadrícula de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3f68-170">Choose hello **Process** tab. On hello Process tab, choose hello default template, under **Build**, choose hello project if it is not already selected, and expand hello **Advanced** section in hello **Build** section of hello grid.</span></span>
6. <span data-ttu-id="d3f68-171">Elija **argumentos de MSBuild**y establezca los argumentos de línea de comandos de MSBuild apropiados Hola tal como se describe en el paso 2 anterior.</span><span class="sxs-lookup"><span data-stu-id="d3f68-171">Choose **MSBuild Arguments**, and set hello appropriate MSBuild command line arguments as described in Step 2 above.</span></span> <span data-ttu-id="d3f68-172">Por ejemplo, escriba **/t: publicar/p: PublishDir =\\\\myserver\\quita\\**  toobuild un paquete de hello empaquetar y copiar archivos de ubicación toohello \\ \\myserver\\quita\\:</span><span class="sxs-lookup"><span data-stu-id="d3f68-172">For example, enter **/t:Publish /p:PublishDir=\\\\myserver\\drops\\** toobuild a package and copy hello package files toohello location \\\\myserver\\drops\\:</span></span>

   ![Argumentos de MSBuild][2]

   > [!NOTE]
   > <span data-ttu-id="d3f68-174">Copiar Hola archivos tooa recurso compartido público facilita toomanually más fácil de implementar paquetes de saludo desde el equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="d3f68-174">Copying hello files tooa public share makes it easier toomanually deploy hello packages from your development computer.</span></span>
7. <span data-ttu-id="d3f68-175">Hola se ha comprobado correctamente el paso de compilación de prueba mediante la comprobación en un proyecto de tooyour de cambio o una nueva compilación en cola.</span><span class="sxs-lookup"><span data-stu-id="d3f68-175">Test hello success of your build step by checking in a change tooyour project, or queue up a new build.</span></span> <span data-ttu-id="d3f68-176">tooqueue de una nueva compilación de Team Explorer, haga clic en **todas las definiciones de compilación,** y, a continuación, elija **poner nueva compilación en cola**.</span><span class="sxs-lookup"><span data-stu-id="d3f68-176">tooqueue up a new build, in the Team Explorer, right-click **All Build Definitions,** and then choose **Queue New Build**.</span></span>

## <a name="4-publish-a-package-using-a-powershell-script"></a><span data-ttu-id="d3f68-177">4: Publicación de un paquete con un script de PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3f68-177">4: Publish a Package using a PowerShell Script</span></span>
<span data-ttu-id="d3f68-178">Esta sección describe cómo tooconstruct una secuencia de comandos de Windows PowerShell que se publicará el paquete de aplicación de nube de hello había salida tooAzure con parámetros opcionales.</span><span class="sxs-lookup"><span data-stu-id="d3f68-178">This section describes how tooconstruct a Windows PowerShell script that will publish hello Cloud app package output tooAzure using optional parameters.</span></span> <span data-ttu-id="d3f68-179">Este script se puede llamar después del paso de compilación de hello en la automatización de compilación personalizada.</span><span class="sxs-lookup"><span data-stu-id="d3f68-179">This script can be called after hello build step in your custom build automation.</span></span> <span data-ttu-id="d3f68-180">También puede llamarse desde las actividades de flujo de trabajo de la Plantilla de procesos en Visual Studio TFS Team Build.</span><span class="sxs-lookup"><span data-stu-id="d3f68-180">It can also be called from Process Template workflow activities in Visual Studio TFS Team Build.</span></span>

1. <span data-ttu-id="d3f68-181">Instalar hello [cmdlets de PowerShell de Azure] [ Azure PowerShell cmdlets] (v0.6.1 o superior).</span><span class="sxs-lookup"><span data-stu-id="d3f68-181">Install hello [Azure PowerShell cmdlets][Azure PowerShell cmdlets] (v0.6.1 or higher).</span></span>
   <span data-ttu-id="d3f68-182">Durante la fase de la instalación de cmdlet de hello, elija tooinstall como un complemento.</span><span class="sxs-lookup"><span data-stu-id="d3f68-182">During hello cmdlet setup phase, choose tooinstall as a snap-in.</span></span> <span data-ttu-id="d3f68-183">Tenga en cuenta que esta versión compatible oficialmente reemplaza la versión anterior de hello ofrecida a través de CodePlex, aunque las versiones anteriores de Hola se numeran 2.x.x.</span><span class="sxs-lookup"><span data-stu-id="d3f68-183">Note that this officially supported version replaces hello older version offered through CodePlex, although hello previous versions were numbered 2.x.x.</span></span>
2. <span data-ttu-id="d3f68-184">Inicie PowerShell de Azure mediante el menú de inicio de Hola o página de inicio.</span><span class="sxs-lookup"><span data-stu-id="d3f68-184">Start Azure PowerShell using hello Start menu or Start page.</span></span> <span data-ttu-id="d3f68-185">Si se inicia en este modo, se cargará Hola cmdlets de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="d3f68-185">If you start in this way, hello Azure PowerShell cmdlets will be loaded.</span></span>
3. <span data-ttu-id="d3f68-186">En el símbolo del sistema de PowerShell hello, verifique que los cmdlets de PowerShell de Hola estén cargados escribiendo el comando parcial de hello `Get-Azure` y, a continuación, presione la tecla Tab para finalización de instrucciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3f68-186">At hello PowerShell prompt, verify that hello PowerShell cmdlets are loaded by entering hello partial command `Get-Azure` and then pressing hello Tab key for statement completion.</span></span>

   <span data-ttu-id="d3f68-187">Si presiona la tecla de la pestaña de hello varias veces, verá varios comandos de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="d3f68-187">If you press hello Tab key repeatedly, you should see various Azure PowerShell commands.</span></span>
4. <span data-ttu-id="d3f68-188">Compruebe que puede conectarse tooyour suscripción de Azure importando la información de suscripción de archivo .publishsettings de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3f68-188">Verify that you can connect tooyour Azure subscription by importing your subscription information from hello .publishsettings file.</span></span>

   `Import-AzurePublishSettingsFile c:\scripts\WindowsAzure\default.publishsettings`

   <span data-ttu-id="d3f68-189">A continuación, escriba el comando de Hola</span><span class="sxs-lookup"><span data-stu-id="d3f68-189">Then enter hello command</span></span>

   `Get-AzureSubscription`

   <span data-ttu-id="d3f68-190">Se muestra información sobre su suscripción.</span><span class="sxs-lookup"><span data-stu-id="d3f68-190">This shows information about your subscription.</span></span> <span data-ttu-id="d3f68-191">Verifique que todo esté correcto.</span><span class="sxs-lookup"><span data-stu-id="d3f68-191">Verify that everything is correct.</span></span>
5. <span data-ttu-id="d3f68-192">Guarde la plantilla de script de Hola Hola final de este artículo a la carpeta de scripts como c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.</span><span class="sxs-lookup"><span data-stu-id="d3f68-192">Save hello script template provided at hello end of this article to your scripts folder as c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.</span></span>
6. <span data-ttu-id="d3f68-193">Revise la sección de parámetros de Hola de script de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3f68-193">Review hello parameters section of hello script.</span></span> <span data-ttu-id="d3f68-194">Agregue o modifique cualquiera de los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="d3f68-194">Add or modify any default values.</span></span> <span data-ttu-id="d3f68-195">Estos valores siempre pueden omitirse al pasar parámetros explícitos.</span><span class="sxs-lookup"><span data-stu-id="d3f68-195">These values can always be overridden by passing in explicit parameters.</span></span>
7. <span data-ttu-id="d3f68-196">Asegúrese de no hay servicios de nube válido y script de publicación de las cuentas de almacenamiento creadas en la suscripción que puede tener como destino Hola.</span><span class="sxs-lookup"><span data-stu-id="d3f68-196">Ensure there are valid cloud service and storage accounts created in your subscription that can be targeted by hello publish script.</span></span> <span data-ttu-id="d3f68-197">La cuenta de almacenamiento (almacenamiento de blobs) se pueden tooupload usado y almacenar temporalmente el archivo de paquete y la configuración de implementación de hello mientras se está creando la implementación.</span><span class="sxs-lookup"><span data-stu-id="d3f68-197">The storage account (blob storage) will be used tooupload and temporarily store hello deployment package and config file while the deployment is being created.</span></span>

   * <span data-ttu-id="d3f68-198">toocreate un nuevo servicio de nube, puede llamar a esta secuencia de comandos o utilice hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d3f68-198">toocreate a new cloud service, you can call this script or use hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="d3f68-199">nombre del servicio de nube de Hola se usará como prefijo un nombre de dominio completo y, por tanto, deben ser único.</span><span class="sxs-lookup"><span data-stu-id="d3f68-199">hello cloud service name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span>

         New-AzureService -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
   * <span data-ttu-id="d3f68-200">toocreate una cuenta de almacenamiento, puede llamar a esta secuencia de comandos o utilice hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d3f68-200">toocreate a new storage account, you can call this script or use hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="d3f68-201">nombre de cuenta de almacenamiento de Hola se usará como prefijo un nombre de dominio completo y, por tanto, deben ser único.</span><span class="sxs-lookup"><span data-stu-id="d3f68-201">hello storage account name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span> <span data-ttu-id="d3f68-202">También puede intentar usar Hola mismo nombre como servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="d3f68-202">You can try using hello same name as the cloud service.</span></span>

         New-AzureStorageAccount -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
8. <span data-ttu-id="d3f68-203">Llame al script de Hola directamente desde PowerShell de Azure, o conecte este toooccur de automatización de compilación de script tooyour host después de la compilación del paquete Hola.</span><span class="sxs-lookup"><span data-stu-id="d3f68-203">Call hello script directly from Azure PowerShell, or wire up this script tooyour host build automation toooccur after hello package build.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="d3f68-204">script de Hola siempre eliminará o reemplazar las implementaciones existentes de forma predeterminada si se detectan.</span><span class="sxs-lookup"><span data-stu-id="d3f68-204">hello script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="d3f68-205">Esto es necesario para habilitar la entrega continua desde la automatización donde no es posible una solicitud del usuario.</span><span class="sxs-lookup"><span data-stu-id="d3f68-205">This is necessary to enable continuous delivery from automation where no user prompting is possible.</span></span>
   >
   >

   <span data-ttu-id="d3f68-206">**Escenario de ejemplo 1:** toohello de implementación continua de un servicio de almacenamiento provisional:</span><span class="sxs-lookup"><span data-stu-id="d3f68-206">**Example scenario 1:** continuous deployment toohello staging environment of a service:</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Staging -serviceName mycloudservice -storageAccountName mystoragesaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="d3f68-207">A esto le sigue generalmente una verificación de ejecución de prueba y un intercambio de VIP.</span><span class="sxs-lookup"><span data-stu-id="d3f68-207">This is typically followed up by test run verification and a VIP swap.</span></span> <span data-ttu-id="d3f68-208">intercambio de VIP de Hello puede hacerse a través de hello [portal de Azure](https://portal.azure.com) o mediante el cmdlet de hello Move-Deployment.</span><span class="sxs-lookup"><span data-stu-id="d3f68-208">hello VIP swap can be done via hello [Azure portal](https://portal.azure.com) or by using hello Move-Deployment cmdlet.</span></span>

   <span data-ttu-id="d3f68-209">**Escenario de ejemplo 2:** entorno de producción de toohello de implementación continua de un servicio de prueba dedicados</span><span class="sxs-lookup"><span data-stu-id="d3f68-209">**Example scenario 2:** continuous deployment toohello production environment of a dedicated test service</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Production -enableDeploymentUpgrade 1 -serviceName mycloudservice -storageAccountName mystorageaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="d3f68-210">**Escritorio remoto:**</span><span class="sxs-lookup"><span data-stu-id="d3f68-210">**Remote Desktop:**</span></span>

   <span data-ttu-id="d3f68-211">Si está habilitado Escritorio remoto en su proyecto de Azure necesitará tooperform los pasos de un solo uso adicionales hello tooensure que correcta certificado del servicio de nube está cargado servicios en la nube tooall objetivo de esta secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="d3f68-211">If Remote Desktop is enabled in your Azure project you will need tooperform additional one-time steps tooensure hello correct Cloud Service Certificate is uploaded tooall cloud services targeted by this script.</span></span>

   <span data-ttu-id="d3f68-212">Buscar valores de huella digital de certificado de hello esperados por sus roles.</span><span class="sxs-lookup"><span data-stu-id="d3f68-212">Locate hello certificate thumbprint values expected by your roles.</span></span> <span data-ttu-id="d3f68-213">Los valores de huella digital son visibles en la sección certificados de hello del archivo de configuración de nube (es decir, ServiceConfiguration.Cloud.cscfg).</span><span class="sxs-lookup"><span data-stu-id="d3f68-213">The thumbprint values are visible in hello Certificates section of the cloud config file (i.e. ServiceConfiguration.Cloud.cscfg).</span></span> <span data-ttu-id="d3f68-214">También es visible en el cuadro de diálogo de configuración de escritorio remoto de hello en Visual Studio cuando Mostrar opciones y ver Hola seleccionado certificado.</span><span class="sxs-lookup"><span data-stu-id="d3f68-214">It is also visible in hello Remote Desktop Configuration dialog in Visual Studio when you Show Options and view hello selected certificate.</span></span>

       <Certificates>
             <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="C33B6C432C25581601B84C80F86EC2809DC224E8" thumbprintAlgorithm="sha1" />
       </Certificates>

   <span data-ttu-id="d3f68-215">Cargar certificados de escritorio remoto como un paso de instalación única mediante Hola siguiente secuencia de comandos de cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d3f68-215">Upload Remote Desktop certificates as a one-time setup step using hello following cmdlet script:</span></span>

       Add-AzureCertificate -serviceName <CLOUDSERVICENAME> -certToDeploy (get-item cert:\CurrentUser\MY\<THUMBPRINT>)

   <span data-ttu-id="d3f68-216">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d3f68-216">For example:</span></span>

       Add-AzureCertificate -serviceName 'mytestcloudservice' -certToDeploy (get-item cert:\CurrentUser\MY\C33B6C432C25581601B84C80F86EC2809DC224E8

   <span data-ttu-id="d3f68-217">O bien puede exportar el archivo de certificado de hello PFX con clave privada y cargar certificados tooeach servicio de destino en la nube utilizando la [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d3f68-217">Alternatively you can export hello certificate file PFX with private key and upload certificates tooeach target cloud service using the [Azure portal](https://portal.azure.com).</span></span>

   <!---
   Fixing broken links for Azure content migration from ACOM tooDOCS. I'm unable toofind a replacement links, so I'm commenting out this reference for now. hello author can investigate in hello future. "Read hello following article toolearn more: http://msdn.microsoft.com/library/windowsazure/gg443832.aspx.
   -->
   <span data-ttu-id="d3f68-218">**Actualizar implementación frente a Eliminar implementación -\> Nueva implementación**</span><span class="sxs-lookup"><span data-stu-id="d3f68-218">**Upgrade Deployment vs. Delete Deployment -\> New Deployment**</span></span>

   <span data-ttu-id="d3f68-219">script de Hola predeterminada realizará una implementación de actualización ($enableDeploymentUpgrade = 1) cuando no se pasa ningún parámetro o el valor 1 se pasa explícitamente.</span><span class="sxs-lookup"><span data-stu-id="d3f68-219">hello script will by default perform an Upgrade Deployment ($enableDeploymentUpgrade = 1) when no parameter is passed in or the value 1 is passed explicitly.</span></span> <span data-ttu-id="d3f68-220">Para las instancias simples, esto tiene la ventaja de tardar menos tiempo que una implementación completa.</span><span class="sxs-lookup"><span data-stu-id="d3f68-220">For single instances this has the advantage of taking less time than a full deployment.</span></span> <span data-ttu-id="d3f68-221">Para instancias que necesitan una alta disponibilidad, que este enfoque también tiene la ventaja de Hola de dejar algunas instancias que se ejecutan mientras que otros están actualizadas (recorrido de su dominio de actualización), además de la dirección VIP no se eliminará.</span><span class="sxs-lookup"><span data-stu-id="d3f68-221">For instances that require high availability this also has hello advantage of leaving some instances running while others are upgraded (walking your update domain), plus your VIP will not be deleted.</span></span>

   <span data-ttu-id="d3f68-222">La implementación de actualización puede deshabilitarse en el script de Hola ($enableDeploymentUpgrade = 0) o pasando *- enableDeploymentUpgrade 0* como un parámetro, que modifica la eliminación de toofirst del comportamiento de script cualquier implementación existente y, a continuación, creará una nueva implementación.</span><span class="sxs-lookup"><span data-stu-id="d3f68-222">Upgrade Deployment can be disabled in hello script ($enableDeploymentUpgrade = 0) or by passing *-enableDeploymentUpgrade 0* as a parameter, which alters the script behavior toofirst delete any existing deployment and then create a new deployment.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="d3f68-223">script de Hola siempre eliminará o reemplazar las implementaciones existentes de forma predeterminada si se detectan.</span><span class="sxs-lookup"><span data-stu-id="d3f68-223">hello script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="d3f68-224">Esto es necesario para habilitar la entrega continua desde la automatización donde no es posible una solicitud del usuario/operador.</span><span class="sxs-lookup"><span data-stu-id="d3f68-224">This is necessary to enable continuous delivery from automation where no user/operator prompting is possible.</span></span>
   >
   >

## <a name="5-publish-a-package-using-tfs-team-build"></a><span data-ttu-id="d3f68-225">5: Publicación de un paquete con TFS Team Build</span><span class="sxs-lookup"><span data-stu-id="d3f68-225">5: Publish a Package using TFS Team Build</span></span>
<span data-ttu-id="d3f68-226">Este paso opcional conecta a TFS Team Build toohello secuencia de comandos creada en el paso 4, que controla la publicación de tooAzure de compilación del paquete de saludo.</span><span class="sxs-lookup"><span data-stu-id="d3f68-226">This optional step connects TFS Team Build toohello script created in step 4, which handles publishing of hello package build tooAzure.</span></span> <span data-ttu-id="d3f68-227">Esto implica Hola Modificar plantilla de proceso utilizada por la definición de compilación para que se ejecute una actividad de publicación final Hola de flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3f68-227">This entails modifying hello Process Template used by your build definition so that it runs a Publish activity at hello end of hello workflow.</span></span> <span data-ttu-id="d3f68-228">Hola publicar actividad ejecutará el comando de PowerShell pasar parámetros de compilación de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3f68-228">hello Publish activity will execute your PowerShell command passing in parameters from hello build.</span></span> <span data-ttu-id="d3f68-229">Salida de hello tiene como destino de MSBuild y script de publicación se canalizará a la salida de compilación estándar de hello.</span><span class="sxs-lookup"><span data-stu-id="d3f68-229">Output of hello MSBuild targets and publish script will be piped into hello standard build output.</span></span>

1. <span data-ttu-id="d3f68-230">Editar definición de compilación responsables de hello continua implementar.</span><span class="sxs-lookup"><span data-stu-id="d3f68-230">Edit hello Build Definition responsible for continuous deploy.</span></span>
2. <span data-ttu-id="d3f68-231">Seleccione hello **proceso** ficha.</span><span class="sxs-lookup"><span data-stu-id="d3f68-231">Select hello **Process** tab.</span></span>
3. <span data-ttu-id="d3f68-232">Siga [estas instrucciones](http://msdn.microsoft.com/library/dd647551.aspx) tooadd un proyecto de actividad para hello plantilla de proceso de compilación, descargar la plantilla predeterminada de hello, agregarlo al proyecto de Hola y lo proteja.</span><span class="sxs-lookup"><span data-stu-id="d3f68-232">Follow [these instructions](http://msdn.microsoft.com/library/dd647551.aspx) tooadd an Activity project for hello build process template, download hello default template, add it to hello project and check it in.</span></span> <span data-ttu-id="d3f68-233">Asigne un nombre nuevo, como AzureBuildProcessTemplate a plantilla de proceso de compilación de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3f68-233">Give hello build process template a new name, such as AzureBuildProcessTemplate.</span></span>
4. <span data-ttu-id="d3f68-234">Devolver toohello **proceso** y a usar **mostrar detalles** tooshow una lista de plantillas de proceso de compilación disponible.</span><span class="sxs-lookup"><span data-stu-id="d3f68-234">Return toohello **Process** tab, and use **Show Details** tooshow a list of available build process templates.</span></span> <span data-ttu-id="d3f68-235">Elija hello **nuevo...**  botón y navegue toohello proyecto que acaba de agrega y protegido.</span><span class="sxs-lookup"><span data-stu-id="d3f68-235">Choose hello **New...** button, and navigate toohello project you just added and checked in.</span></span> <span data-ttu-id="d3f68-236">Busque la plantilla de Hola que acaba de crear y elija **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="d3f68-236">Locate hello template you just created and choose **OK**.</span></span>
5. <span data-ttu-id="d3f68-237">Hola abierto había seleccionado la plantilla de proceso para su edición.</span><span class="sxs-lookup"><span data-stu-id="d3f68-237">Open hello selected Process Template for editing.</span></span> <span data-ttu-id="d3f68-238">Puede abrir directamente en el Diseñador de flujo de trabajo de Hola o en hello toowork de editor de XML con hello XAML.</span><span class="sxs-lookup"><span data-stu-id="d3f68-238">You can open directly in hello Workflow designer or in hello XML editor toowork with hello XAML.</span></span>
6. <span data-ttu-id="d3f68-239">Agregar Hola siguiendo la lista de argumentos nuevos como partidas separadas en la ficha de argumentos de hello del Diseñador de flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3f68-239">Add hello following list of new arguments as separate line items in hello arguments tab of hello workflow designer.</span></span> <span data-ttu-id="d3f68-240">Todos los argumentos deben tener la dirección=In y el tipo=String.</span><span class="sxs-lookup"><span data-stu-id="d3f68-240">All arguments should have direction=In and type=String.</span></span> <span data-ttu-id="d3f68-241">Estos serán tooflow usa parámetros de definición de compilación de hello en flujo de trabajo de hello, qué Hola de toocall usa get, a continuación, el script de publicación.</span><span class="sxs-lookup"><span data-stu-id="d3f68-241">These will be used tooflow parameters from hello build definition into hello workflow, which then get used toocall hello publish script.</span></span>

       SubscriptionName
       StorageAccountName
       CloudConfigLocation
       PackageLocation
       Environment
       SubscriptionDataFileLocation
       PublishScriptLocation
       ServiceName

   ![Lista de argumentos][3]

   <span data-ttu-id="d3f68-243">Hola que XAML correspondiente tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="d3f68-243">hello corresponding XAML looks like this:</span></span>

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
7. <span data-ttu-id="d3f68-244">Agregue una nueva secuencia final Hola de ejecutar en el agente:</span><span class="sxs-lookup"><span data-stu-id="d3f68-244">Add a new sequence at hello end of Run On Agent:</span></span>

   1. <span data-ttu-id="d3f68-245">Empiece agregando un toocheck de actividad de instrucción If para un archivo de script válido.</span><span class="sxs-lookup"><span data-stu-id="d3f68-245">Start by adding an If Statement activity toocheck for a valid script file.</span></span> <span data-ttu-id="d3f68-246">Establecer el valor de toothis de hello condición:</span><span class="sxs-lookup"><span data-stu-id="d3f68-246">Set hello condition toothis value:</span></span>

          Not String.IsNullOrEmpty(PublishScriptLocation)
   2. <span data-ttu-id="d3f68-247">Hola, a continuación, caso de hello instrucción If, agregue una nueva actividad de secuencia.</span><span class="sxs-lookup"><span data-stu-id="d3f68-247">In hello Then case of hello If Statement, add a new Sequence activity.</span></span> <span data-ttu-id="d3f68-248">Publicar conjunto Hola Mostrar nombre too'Start'</span><span class="sxs-lookup"><span data-stu-id="d3f68-248">Set hello display name too'Start publish'</span></span>
   3. <span data-ttu-id="d3f68-249">Con hello inicio publicar secuencia aún seleccionado, agregue la siguiente lista de nuevas variables como elementos de línea independientes en la pestaña variables de diseñador de flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3f68-249">With hello Start publish sequence still selected, add the following list of new variables as separate line items in the variables tab of hello workflow designer.</span></span> <span data-ttu-id="d3f68-250">Todas las variables deben tener el tipo de variable =Cadena y el ámbito =Iniciar publicación.</span><span class="sxs-lookup"><span data-stu-id="d3f68-250">All variables should have Variable type =String and Scope=Start publish.</span></span> <span data-ttu-id="d3f68-251">Estos serán tooflow usa parámetros de definición de compilación de hello en el flujo de trabajo, que, a continuación, hello toocall usado de get script de publicación.</span><span class="sxs-lookup"><span data-stu-id="d3f68-251">These will be used tooflow parameters from hello build definition into the workflow, which then get used toocall hello publish script.</span></span>

      * <span data-ttu-id="d3f68-252">SubscriptionDataFilePath, de tipo Cadena</span><span class="sxs-lookup"><span data-stu-id="d3f68-252">SubscriptionDataFilePath, of type String</span></span>
      * <span data-ttu-id="d3f68-253">PublishScriptFilePath, de tipo Cadena</span><span class="sxs-lookup"><span data-stu-id="d3f68-253">PublishScriptFilePath, of type String</span></span>

        ![Nuevas variables][4]
   4. <span data-ttu-id="d3f68-255">Si usa TFS 2012 o versiones anteriores, agregar una actividad ConvertWorkspaceItem Hola principio de Hola nueva secuencia.</span><span class="sxs-lookup"><span data-stu-id="d3f68-255">If you are using TFS 2012 or earlier, add a ConvertWorkspaceItem activity at hello beginning of hello new Sequence.</span></span> <span data-ttu-id="d3f68-256">Si usa TFS 2013 o versiones posteriores, agregar una actividad GetLocalPath Hola principio de la nueva secuencia de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3f68-256">If you are using TFS 2013 or later, add a GetLocalPath activity at hello beginning of hello new sequence.</span></span> <span data-ttu-id="d3f68-257">Para una ConvertWorkspaceItem, establecer las propiedades de hello como sigue: dirección = ServerToLocal, DisplayName = 'Convert publicar nombre de archivo de script,' entrada = 'PublishScriptLocation', resultado = 'PublishScriptFilePath', el área de trabajo = 'Área de trabajo'.</span><span class="sxs-lookup"><span data-stu-id="d3f68-257">For a ConvertWorkspaceItem, set hello properties as follows: Direction=ServerToLocal, DisplayName='Convert publish script filename', Input=' PublishScriptLocation', Result='PublishScriptFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="d3f68-258">Para una actividad GetLocalPath, establecer Hola propiedad IncomingPath too'PublishScriptLocation', y Hola resultado too'PublishScriptFilePath'.</span><span class="sxs-lookup"><span data-stu-id="d3f68-258">For a GetLocalPath activity, set hello property IncomingPath too'PublishScriptLocation', and hello Result too'PublishScriptFilePath'.</span></span> <span data-ttu-id="d3f68-259">Esta toohello de ruta de acceso de actividad convierte Hola script desde ubicaciones de servidor TFS de publicación (si procede) tooa ruta de acceso del disco local estándar.</span><span class="sxs-lookup"><span data-stu-id="d3f68-259">This activity converts hello path toohello publish script from TFS server locations (if applicable) tooa standard local disk path.</span></span>
   5. <span data-ttu-id="d3f68-260">Si usa TFS 2012 o versiones anteriores, agregue otra actividad ConvertWorkspaceItem final Hola de Hola nueva secuencia.</span><span class="sxs-lookup"><span data-stu-id="d3f68-260">If you are using TFS 2012 or earlier, add another ConvertWorkspaceItem activity at hello end of hello new Sequence.</span></span> <span data-ttu-id="d3f68-261">Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'.</span><span class="sxs-lookup"><span data-stu-id="d3f68-261">Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="d3f68-262">Si está utilizando TFS 2013 o posterior, agregue otro GetLocalPath.</span><span class="sxs-lookup"><span data-stu-id="d3f68-262">If you are using TFS 2013 or later, add another GetLocalPath.</span></span> <span data-ttu-id="d3f68-263">IncomingPath='SubscriptionDataFileLocation' y Result='SubscriptionDataFilePath.'</span><span class="sxs-lookup"><span data-stu-id="d3f68-263">IncomingPath='SubscriptionDataFileLocation', and Result='SubscriptionDataFilePath.'</span></span>
   6. <span data-ttu-id="d3f68-264">Agregue una actividad InvokeProcess final Hola de hello nueva secuencia.</span><span class="sxs-lookup"><span data-stu-id="d3f68-264">Add an InvokeProcess activity at hello end of hello new Sequence.</span></span>
      <span data-ttu-id="d3f68-265">Esta llamadas de actividad PowerShell.exe con hello argumentos pasan por Hola definición de compilación.</span><span class="sxs-lookup"><span data-stu-id="d3f68-265">This activity calls PowerShell.exe with hello arguments passed in by hello Build Definition.</span></span>

      + <span data-ttu-id="d3f68-266">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span><span class="sxs-lookup"><span data-stu-id="d3f68-266">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span></span>
      + <span data-ttu-id="d3f68-267">DisplayName =Ejecutar script de publicación</span><span class="sxs-lookup"><span data-stu-id="d3f68-267">DisplayName = Execute publish script</span></span>
      + <span data-ttu-id="d3f68-268">FileName = "PowerShell" (incluya comillas hello)</span><span class="sxs-lookup"><span data-stu-id="d3f68-268">FileName = "PowerShell" (include hello quotes)</span></span>
      + <span data-ttu-id="d3f68-269">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span><span class="sxs-lookup"><span data-stu-id="d3f68-269">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span></span>
   7. <span data-ttu-id="d3f68-270">Hola **controlar la salida estándar** sección cuadro de texto de la InvokeProcess, establezca Hola cuadro de texto valor too'data'.</span><span class="sxs-lookup"><span data-stu-id="d3f68-270">In hello **Handle Standard Output** section textbox of the InvokeProcess, set hello textbox value too'data'.</span></span> <span data-ttu-id="d3f68-271">Se trata de una salida estándar de hello toostore variable datos.</span><span class="sxs-lookup"><span data-stu-id="d3f68-271">This is a variable toostore hello standard output data.</span></span>
   8. <span data-ttu-id="d3f68-272">Agregar una actividad WriteBuildMessage justo debajo de hello **controlar la salida estándar** sección.</span><span class="sxs-lookup"><span data-stu-id="d3f68-272">Add a WriteBuildMessage activity just below hello **Handle Standard Output** section.</span></span> <span data-ttu-id="d3f68-273">Establecer la importancia de hello = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' y Hola mensaje = 'data'.</span><span class="sxs-lookup"><span data-stu-id="d3f68-273">Set hello Importance = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' and hello Message='data'.</span></span> <span data-ttu-id="d3f68-274">Esto garantiza que la salida estándar de hello de la secuencia de comandos obtener escribirán toohello resultados de la compilación.</span><span class="sxs-lookup"><span data-stu-id="d3f68-274">This ensures hello standard output of the script will get written toohello build output.</span></span>
   9. <span data-ttu-id="d3f68-275">Hola **controlar la salida de Error** sección cuadro de texto de la InvokeProcess, establezca Hola cuadro de texto valor too'data'.</span><span class="sxs-lookup"><span data-stu-id="d3f68-275">In hello **Handle Error Output** section textbox of the InvokeProcess, set hello textbox value too'data'.</span></span> <span data-ttu-id="d3f68-276">Se trata de un datos de error estándar de hello toostore variable.</span><span class="sxs-lookup"><span data-stu-id="d3f68-276">This is a variable toostore hello standard error data.</span></span>
   10. <span data-ttu-id="d3f68-277">Agregar una actividad WriteBuildError justo debajo de hello **controlar la salida de Error** sección.</span><span class="sxs-lookup"><span data-stu-id="d3f68-277">Add a WriteBuildError activity just below hello **Handle Error Output** section.</span></span> <span data-ttu-id="d3f68-278">Establecer Hola mensaje = 'data'.</span><span class="sxs-lookup"><span data-stu-id="d3f68-278">Set hello Message='data'.</span></span> <span data-ttu-id="d3f68-279">Esto garantiza la salida de error de compilación toohello obtener escribirán Hola estándar errores de script de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3f68-279">This ensures hello standard errors of hello script will get written toohello build error output.</span></span>
   11. <span data-ttu-id="d3f68-280">Corrija los errores, que se indican por signos de exclamación azules.</span><span class="sxs-lookup"><span data-stu-id="d3f68-280">Correct any errors, indicated by blue exclamation marks.</span></span> <span data-ttu-id="d3f68-281">Mantenga el mouse sobre el tooget signos de exclamación una sugerencia sobre el error de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3f68-281">Hover over the exclamation marks tooget a hint about hello error.</span></span> <span data-ttu-id="d3f68-282">Guardar el flujo de trabajo de Hola para borrar los errores.</span><span class="sxs-lookup"><span data-stu-id="d3f68-282">Save hello workflow to clear errors.</span></span>

   <span data-ttu-id="d3f68-283">resultado final de Hola de hello publicar actividades tendrá un aspecto similar al siguiente en el Diseñador de Hola de flujo de trabajo:</span><span class="sxs-lookup"><span data-stu-id="d3f68-283">hello final result of hello publish workflow activities will look like this in hello designer:</span></span>

   ![Actividades de flujo de trabajo][5]

   <span data-ttu-id="d3f68-285">resultado final de Hola de hello publicar actividades tendrá un aspecto similar al siguiente en XAML de flujo de trabajo:</span><span class="sxs-lookup"><span data-stu-id="d3f68-285">hello final result of hello publish workflow activities will look like this in XAML:</span></span>

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
8. <span data-ttu-id="d3f68-286">Guarde el flujo de trabajo de plantilla de proceso de compilación de Hola y proteger este archivo.</span><span class="sxs-lookup"><span data-stu-id="d3f68-286">Save hello build process template workflow and Check In this file.</span></span>
9. <span data-ttu-id="d3f68-287">Editar definición de compilación de hello (cerrarla si ya está abierto), seleccione hello y **New** botón si aún no ve nueva plantilla de hello en lista de Hola de plantillas de proceso.</span><span class="sxs-lookup"><span data-stu-id="d3f68-287">Edit hello build definition (close it if it is already open), and select hello **New** button if you do not yet see hello new template in hello list of Process Templates.</span></span>
10. <span data-ttu-id="d3f68-288">Establecer valores de propiedad de parámetro de Hola Hola sección adicional de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="d3f68-288">Set hello parameter property values in hello Misc section as follows:</span></span>

    1. <span data-ttu-id="d3f68-289">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *Este valor se obtiene de: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span><span class="sxs-lookup"><span data-stu-id="d3f68-289">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *This value is derived from: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span></span>
    2. <span data-ttu-id="d3f68-290">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *Este valor se obtiene de:($PublishDir)($ProjectName).cspkg*</span><span class="sxs-lookup"><span data-stu-id="d3f68-290">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *This value is derived from: ($PublishDir)($ProjectName).cspkg*</span></span>
    3. <span data-ttu-id="d3f68-291">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span><span class="sxs-lookup"><span data-stu-id="d3f68-291">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span></span>
    4. <span data-ttu-id="d3f68-292">ServiceName = 'mycloudservicename' *usar Hola nube adecuada servicio el nombre aquí*</span><span class="sxs-lookup"><span data-stu-id="d3f68-292">ServiceName = 'mycloudservicename' *Use hello appropriate cloud service name here*</span></span>
    5. <span data-ttu-id="d3f68-293">Entorno = 'Staging'</span><span class="sxs-lookup"><span data-stu-id="d3f68-293">Environment = 'Staging'</span></span>
    6. <span data-ttu-id="d3f68-294">StorageAccountName = 'mystorageaccountname' *usar Hola almacenamiento adecuado cuenta el nombre aquí*</span><span class="sxs-lookup"><span data-stu-id="d3f68-294">StorageAccountName = 'mystorageaccountname' *Use hello appropriate storage account name here*</span></span>
    7. <span data-ttu-id="d3f68-295">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span><span class="sxs-lookup"><span data-stu-id="d3f68-295">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span></span>
    8. <span data-ttu-id="d3f68-296">SubscriptionName = 'default'</span><span class="sxs-lookup"><span data-stu-id="d3f68-296">SubscriptionName = 'default'</span></span>

    ![Valores de propiedad de parámetro][6]
11. <span data-ttu-id="d3f68-298">Guardar cambios de hello toohello definición de compilación.</span><span class="sxs-lookup"><span data-stu-id="d3f68-298">Save hello changes toohello Build Definition.</span></span>
12. <span data-ttu-id="d3f68-299">Poner en cola un tooexecute compilación ambos Hola compilación del paquete y publicación.</span><span class="sxs-lookup"><span data-stu-id="d3f68-299">Queue a Build tooexecute both hello package build and publish.</span></span> <span data-ttu-id="d3f68-300">Si tiene un desencadenador establecer tooContinuous integración, se ejecutará este comportamiento en cada protección.</span><span class="sxs-lookup"><span data-stu-id="d3f68-300">If you have a trigger set tooContinuous Integration, you will execute this behavior on every check-in.</span></span>

### <a name="publishcloudserviceps1-script-template"></a><span data-ttu-id="d3f68-301">Plantilla de script PublishCloudService.ps1</span><span class="sxs-lookup"><span data-stu-id="d3f68-301">PublishCloudService.ps1 script template</span></span>
```
Param(  $serviceName = "",
        $storageAccountName = "",
        $packageLocation = "",
        $cloudConfigLocation = "",
        $environment = "Staging",
        $deploymentLabel = "ContinuousDeploy too$servicename",
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
    #check for existing deployment and then either upgrade, delete + deploy, or cancel according too$alwaysDeleteExistingDeployments and $enableDeploymentUpgrade boolean variables
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

#main driver - publish & write progress tooactivity log
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script started."
Write-Output "$(Get-Date -f $timeStampFormat) - Preparing deployment of $deploymentLabel for $subscriptionname with Subscription ID $subscriptionid."

Publish

$deployment = Get-AzureDeployment -slot $slot -serviceName $servicename
$deploymentUrl = $deployment.Url

Write-Output "$(Get-Date -f $timeStampFormat) - Created Cloud Service with URL $deploymentUrl."
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script finished."
```

## <a name="next-steps"></a><span data-ttu-id="d3f68-302">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d3f68-302">Next steps</span></span>
<span data-ttu-id="d3f68-303">depuración remota de tooenable cuando se utiliza la entrega continua, vea [habilitar la depuración remota al utilizar la entrega continua toopublish tooAzure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span><span class="sxs-lookup"><span data-stu-id="d3f68-303">tooenable remote debugging when using continuous delivery, see [Enable remote debugging when using continuous delivery toopublish tooAzure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span></span>

[Team Foundation Build Service]: https://msdn.microsoft.com/library/ee259687.aspx
[.NET Framework 4]: https://www.microsoft.com/download/details.aspx?id=17851
[.NET Framework 4.5]: https://www.microsoft.com/download/details.aspx?id=30653
[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42643
[Scale out your build system]: https://msdn.microsoft.com/library/dd793166.aspx
[Deploy and configure a build server]: https://msdn.microsoft.com/library/ms181712.aspx
[Azure PowerShell cmdlets]: /powershell/azureps-cmdlets-docs
[hello .publishsettings file]: https://manage.windowsazure.com/download/publishprofile.aspx?wa=wsignin1.0
[0]: ./media/cloud-services-dotnet-continuous-delivery/tfs-01bc.png
[2]: ./media/cloud-services-dotnet-continuous-delivery/tfs-02.png
[3]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-03.png
[4]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-04.png
[5]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-05.png
[6]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-06.png
