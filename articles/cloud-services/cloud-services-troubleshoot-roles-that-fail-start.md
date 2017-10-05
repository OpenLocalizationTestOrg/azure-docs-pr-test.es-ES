---
title: "Solución de problemas de roles que no se inician| Microsoft Docs"
description: "A continuación, se indican algunas causas habituales por las que un rol de servicio en la nube puede no iniciarse. También se proporcionan soluciones a estos problemas."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 674b2faf-26d7-4f54-99ea-a9e02ef0eb2f
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 7d956192e8b9c3688b8b6f0108bd9296f66fbd62
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-cloud-service-roles-that-fail-to-start"></a><span data-ttu-id="6d9ee-104">Solución de problemas de roles de servicios en la nube que no se inician</span><span class="sxs-lookup"><span data-stu-id="6d9ee-104">Troubleshoot Cloud Service roles that fail to start</span></span>
<span data-ttu-id="6d9ee-105">Presentamos algunos problemas y soluciones comunes relacionados con los roles de los servicios en la nube de Azure que no se inician.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-105">Here are some common problems and solutions related to Azure Cloud Services roles that fail to start.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-dlls-or-dependencies"></a><span data-ttu-id="6d9ee-106">DLL o dependencias que faltan</span><span class="sxs-lookup"><span data-stu-id="6d9ee-106">Missing DLLs or dependencies</span></span>
<span data-ttu-id="6d9ee-107">Tanto que los roles no respondan como que alternen entre los estados **Inicializando**, **Ocupado** y **Deteniendo** puede deberse a que faltan DLL o ensamblados.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-107">Unresponsive roles and roles that are cycling between **Initializing**, **Busy**, and **Stopping** states can be caused by missing DLLs or assemblies.</span></span>

<span data-ttu-id="6d9ee-108">Estos son los síntomas de que faltan DLL o ensamblados:</span><span class="sxs-lookup"><span data-stu-id="6d9ee-108">Symptoms of missing DLLs or assemblies can be:</span></span>

* <span data-ttu-id="6d9ee-109">Una instancia de rol alterna entre los estados **Inicializando**, **Ocupado** y **Deteniendo**.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-109">Your role instance is cycling through **Initializing**, **Busy**, and **Stopping** states.</span></span>
* <span data-ttu-id="6d9ee-110">La instancia de rol se ha movido al estado **Listo** , pero si se navega a la aplicación web, la página no aparece.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-110">Your role instance has moved to **Ready** but if you navigate to your web application, the page does not appear.</span></span>

<span data-ttu-id="6d9ee-111">Hay varios métodos recomendados para investigar estos problemas.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-111">There are several recommended methods for investigating these issues.</span></span>

## <a name="diagnose-missing-dll-issues-in-a-web-role"></a><span data-ttu-id="6d9ee-112">Diagnóstico del problema de DLL que faltan en un rol web</span><span class="sxs-lookup"><span data-stu-id="6d9ee-112">Diagnose missing DLL issues in a web role</span></span>
<span data-ttu-id="6d9ee-113">Cuando se navega a un sitio web que se implementa en un rol web y el explorador muestra un error de servidor similar al siguiente, puede significar que falta alguna DLL.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-113">When you navigate to a website that is deployed in a web role, and the browser displays a server error similar to the following, it may indicate that a DLL is missing.</span></span>

![Error del servidor en la aplicación '/'](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503388.png)

## <a name="diagnose-issues-by-turning-off-custom-errors"></a><span data-ttu-id="6d9ee-115">Diagnóstico de problemas mediante la desactivación de errores personalizados</span><span class="sxs-lookup"><span data-stu-id="6d9ee-115">Diagnose issues by turning off custom errors</span></span>
<span data-ttu-id="6d9ee-116">Para ver una información más completa de los errores, configure el archivo web.config del rol web estableciendo el modo de error personalizado en desactivado y vuelva a implementar el servicio.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-116">More complete error information can be viewed by configuring the web.config for the web role to set the custom error mode to Off and redeploying the service.</span></span>

<span data-ttu-id="6d9ee-117">Para ver más errores completos sin usar Escritorio remoto:</span><span class="sxs-lookup"><span data-stu-id="6d9ee-117">To view more complete errors without using Remote Desktop:</span></span>

1. <span data-ttu-id="6d9ee-118">Abra la solución en Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-118">Open the solution in Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="6d9ee-119">En el **Explorador de soluciones**, busque el archivo web.config y ábralo.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-119">In the **Solution Explorer**, locate the web.config file and open it.</span></span>
3. <span data-ttu-id="6d9ee-120">En el archivo web.config, busque la sección system.web y agregue la siguiente línea:</span><span class="sxs-lookup"><span data-stu-id="6d9ee-120">In the web.config file, locate the system.web section and add the following line:</span></span>

    ```xml
    <customErrors mode="Off" />
    ```
4. <span data-ttu-id="6d9ee-121">Guarde el archivo .</span><span class="sxs-lookup"><span data-stu-id="6d9ee-121">Save the file.</span></span>
5. <span data-ttu-id="6d9ee-122">Vuelva a empaquetar e implementar el servicio.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-122">Repackage and redeploy the service.</span></span>

<span data-ttu-id="6d9ee-123">Una vez que se vuelva a implementar el servicio, verá un mensaje de error con el nombre del ensamblado o DLL que faltan.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-123">Once the service is redeployed, you will see an error message with the name of the missing assembly or DLL.</span></span>

## <a name="diagnose-issues-by-viewing-the-error-remotely"></a><span data-ttu-id="6d9ee-124">Diagnóstico de problemas mediante la comprobación del error de forma remota</span><span class="sxs-lookup"><span data-stu-id="6d9ee-124">Diagnose issues by viewing the error remotely</span></span>
<span data-ttu-id="6d9ee-125">Puede usar Escritorio remoto para acceder al rol y ver información más completa sobre los errores de forma remota.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-125">You can use Remote Desktop to access the role and view more complete error information remotely.</span></span> <span data-ttu-id="6d9ee-126">Use los pasos siguientes para ver los errores desde Escritorio remoto:</span><span class="sxs-lookup"><span data-stu-id="6d9ee-126">Use the following steps to view the errors by using Remote Desktop:</span></span>

1. <span data-ttu-id="6d9ee-127">Asegúrese de que está instalado el SDK 1.3 de Azure, o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-127">Ensure that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="6d9ee-128">Durante la implementación de la solución con Visual Studio, elija "Configurar conexiones a Escritorio remoto...".</span><span class="sxs-lookup"><span data-stu-id="6d9ee-128">During the deployment of the solution by using Visual Studio, choose to “Configure Remote Desktop connections…”.</span></span> <span data-ttu-id="6d9ee-129">Para más información sobre cómo configurar la conexión a Escritorio remoto, consulte [Uso de Escritorio remoto con los roles de Azure](../vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="6d9ee-129">For more information on configuring the Remote Desktop connection, see [Using Remote Desktop with Azure Roles](../vs-azure-tools-remote-desktop-roles.md).</span></span>
3. <span data-ttu-id="6d9ee-130">En el Portal de Microsoft Azure clásico, cuando la instancia muestre el estado **Listo**, haga clic en una de las instancias de rol.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-130">In the Microsoft Azure classic portal, once the instance shows a status of **Ready**, click one of the role instances.</span></span>
4. <span data-ttu-id="6d9ee-131">Haga clic en el icono **Conectar** del área **Acceso remoto** de la cinta de opciones.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-131">Click the **Connect** icon in the **Remote Access** area of the ribbon.</span></span>
5. <span data-ttu-id="6d9ee-132">Inicie sesión en la máquina virtual con las credenciales especificadas en la configuración de Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-132">Sign in to the virtual machine by using the credentials that were specified during the Remote Desktop configuration.</span></span>
6. <span data-ttu-id="6d9ee-133">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-133">Open a command window.</span></span>
7. <span data-ttu-id="6d9ee-134">Escriba `IPconfig`.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-134">Type `IPconfig`.</span></span>
8. <span data-ttu-id="6d9ee-135">Anote el valor de dirección IPV4.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-135">Note the IPV4 Address value.</span></span>
9. <span data-ttu-id="6d9ee-136">Abra Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-136">Open Internet Explorer.</span></span>
10. <span data-ttu-id="6d9ee-137">Escriba la dirección y el nombre de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-137">Type the address and the name of the web application.</span></span> <span data-ttu-id="6d9ee-138">Por ejemplo: `http://<IPV4 Address>/default.aspx`.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-138">For example, `http://<IPV4 Address>/default.aspx`.</span></span>

<span data-ttu-id="6d9ee-139">Si navega al sitio web, se devolverán mensajes de error más explícitos:</span><span class="sxs-lookup"><span data-stu-id="6d9ee-139">Navigating to the website will now return more explicit error messages:</span></span>

* <span data-ttu-id="6d9ee-140">Error del servidor en la aplicación '/'</span><span class="sxs-lookup"><span data-stu-id="6d9ee-140">Server Error in '/' Application.</span></span>
* <span data-ttu-id="6d9ee-141">Descripción: Se produjo una excepción no controlada durante la ejecución de la solicitud web actual.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-141">Description: An unhandled exception occurred during the execution of the current web request.</span></span> <span data-ttu-id="6d9ee-142">Revise el seguimiento de la pila para obtener más información acerca del error y en donde se originó en el código.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-142">Please review the stack trace for more information about the error and where it originated in the code.</span></span>
* <span data-ttu-id="6d9ee-143">Detalles de la excepción: System.IO.FIleNotFoundException: No se puede cargar el archivo o ensamblado ‘Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35’ ni una de sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-143">Exception Details: System.IO.FIleNotFoundException: Could not load file or assembly ‘Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35’ or one of its dependencies.</span></span> <span data-ttu-id="6d9ee-144">El sistema no encuentra el archivo especificado.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-144">The system cannot find the file specified.</span></span>

<span data-ttu-id="6d9ee-145">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6d9ee-145">For example:</span></span>

![Error explícito del servidor en la aplicación '/'](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503389.png)

## <a name="diagnose-issues-by-using-the-compute-emulator"></a><span data-ttu-id="6d9ee-147">Diagnóstico de problemas mediante el emulador de proceso</span><span class="sxs-lookup"><span data-stu-id="6d9ee-147">Diagnose issues by using the compute emulator</span></span>
<span data-ttu-id="6d9ee-148">El emulador de proceso de Microsoft Azure se puede usar para diagnosticar y solucionar problemas de errores en web.config y dependencias que faltan.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-148">You can use the Microsoft Azure compute emulator to diagnose and troubleshoot issues of missing dependencies and web.config errors.</span></span>

<span data-ttu-id="6d9ee-149">Para obtener unos mejores resultados con este método de diagnóstico, debe usar un equipo o máquina virtual que tenga una instalación limpia de Windows.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-149">For best results in using this method of diagnosis, you should use a computer or virtual machine that has a clean installation of Windows.</span></span> <span data-ttu-id="6d9ee-150">Para simular lo mejor posible el entorno de Azure, use Windows Server 2008 R2 x64.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-150">To best simulate the Azure environment, use Windows Server 2008 R2 x64.</span></span>

1. <span data-ttu-id="6d9ee-151">Instale la versión independiente de [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="6d9ee-151">Install the standalone version of the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="6d9ee-152">En la máquina de desarrollo, compile el proyecto de servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-152">On the development machine, build the cloud service project.</span></span>
3. <span data-ttu-id="6d9ee-153">En el Explorador de Windows, desplácese a la carpeta bin\debug del proyecto del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-153">In Windows Explorer, navigate to the bin\debug folder of the cloud service project.</span></span>
4. <span data-ttu-id="6d9ee-154">Copie la carpeta .csx y el archivo .cscfg en el equipo que se usa para depurar los problemas.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-154">Copy the .csx folder and .cscfg file to the computer that you are using to debug the issues.</span></span>
5. <span data-ttu-id="6d9ee-155">En la máquina limpia, abra una ventana del símbolo del sistema del SDK de Azure y escriba `csrun.exe /devstore:start`.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-155">On the clean machine, open an Azure SDK Command Prompt window and type `csrun.exe /devstore:start`.</span></span>
6. <span data-ttu-id="6d9ee-156">En el símbolo del sistema, escriba `run csrun <path to .csx folder> <path to .cscfg file> /launchBrowser`.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-156">At the command prompt, type `run csrun <path to .csx folder> <path to .cscfg file> /launchBrowser`.</span></span>
7. <span data-ttu-id="6d9ee-157">Cuando se inicie el rol, verá información detallada del error en Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-157">When the role starts, you will see detailed error information in Internet Explorer.</span></span> <span data-ttu-id="6d9ee-158">También puede usar las herramientas de solución de problemas estándar de Windows para efectuar un diagnóstico exhaustivo del problema.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-158">You can also use standard Windows troubleshooting tools to further diagnose the problem.</span></span>

## <a name="diagnose-issues-by-using-intellitrace"></a><span data-ttu-id="6d9ee-159">Diagnóstico de problemas mediante IntelliTrace</span><span class="sxs-lookup"><span data-stu-id="6d9ee-159">Diagnose issues by using IntelliTrace</span></span>
<span data-ttu-id="6d9ee-160">Para los roles web y de trabajo que usan .NET Framework 4, puede usar [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), que está disponible en Microsoft Visual Studio Enterprise.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-160">For worker and web roles that use .NET Framework 4, you can use [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), which is available in Microsoft Visual Studio Enterprise.</span></span>

<span data-ttu-id="6d9ee-161">Siga estos pasos para implementar el servicio con IntelliTrace habilitado:</span><span class="sxs-lookup"><span data-stu-id="6d9ee-161">Follow these steps to deploy the service with IntelliTrace enabled:</span></span>

1. <span data-ttu-id="6d9ee-162">Confirme que está instalado el SDK 1.3 de Azure, o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-162">Confirm that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="6d9ee-163">Implemente la solución con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-163">Deploy the solution by using Visual Studio.</span></span> <span data-ttu-id="6d9ee-164">Durante la implementación, active la casilla **Habilitar IntelliTrace para roles de .NET 4** .</span><span class="sxs-lookup"><span data-stu-id="6d9ee-164">During deployment, check the **Enable IntelliTrace for .NET 4 roles** check box.</span></span>
3. <span data-ttu-id="6d9ee-165">Una vez que se inicia la instancia, abra el **Explorador de servidores**.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-165">Once the instance starts, open the **Server Explorer**.</span></span>
4. <span data-ttu-id="6d9ee-166">Expanda el nodo **Azure\\Cloud Services** y busque la implementación.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-166">Expand the **Azure\\Cloud Services** node and locate the deployment.</span></span>
5. <span data-ttu-id="6d9ee-167">Expanda la implementación hasta que vea las instancias de rol.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-167">Expand the deployment until you see the role instances.</span></span> <span data-ttu-id="6d9ee-168">Haga clic con el botón derecho en una de las instancias.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-168">Right-click on one of the instances.</span></span>
6. <span data-ttu-id="6d9ee-169">Elija **Ver registros de IntelliTrace**.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-169">Choose **View IntelliTrace logs**.</span></span> <span data-ttu-id="6d9ee-170">Se abrirá el **resumen de IntelliTrace** .</span><span class="sxs-lookup"><span data-stu-id="6d9ee-170">The **IntelliTrace Summary** will open.</span></span>
7. <span data-ttu-id="6d9ee-171">Busque la sección de excepciones del resumen.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-171">Locate the exceptions section of the summary.</span></span> <span data-ttu-id="6d9ee-172">Si hay excepciones, se denominará **Datos de excepción**.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-172">If there are exceptions, the section will be labeled **Exception Data**.</span></span>
8. <span data-ttu-id="6d9ee-173">Expanda los **datos de excepción** y busque errores **System.IO.FileNotFoundException** similares al siguiente:</span><span class="sxs-lookup"><span data-stu-id="6d9ee-173">Expand the **Exception Data** and look for **System.IO.FileNotFoundException** errors similar to the following:</span></span>

![Datos de excepción, faltan archivo o ensamblado](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503390.png)

## <a name="address-missing-dlls-and-assemblies"></a><span data-ttu-id="6d9ee-175">Tratamiento de archivos DLL y ensamblados que faltan</span><span class="sxs-lookup"><span data-stu-id="6d9ee-175">Address missing DLLs and assemblies</span></span>
<span data-ttu-id="6d9ee-176">Para tratar los errores de ensamblado y de DLL que faltan, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="6d9ee-176">To address missing DLL and assembly errors, follow these steps:</span></span>

1. <span data-ttu-id="6d9ee-177">Abra la solución en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-177">Open the solution in Visual Studio.</span></span>
2. <span data-ttu-id="6d9ee-178">En el **Explorador de soluciones**, abra la carpeta **Referencias**.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-178">In **Solution Explorer**, open the **References** folder.</span></span>
3. <span data-ttu-id="6d9ee-179">Haga clic en el ensamblado identificado en el error.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-179">Click the assembly identified in the error.</span></span>
4. <span data-ttu-id="6d9ee-180">En el panel **Propiedades**, busque la **propiedad Copy Local** y establezca su valor en **True**.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-180">In the **Properties** pane, locate **Copy Local property** and set the value to **True**.</span></span>
5. <span data-ttu-id="6d9ee-181">Vuelva a implementar el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-181">Redeploy the cloud service.</span></span>

<span data-ttu-id="6d9ee-182">Cuando haya comprobado que se han corregido todos los errores, se puede implementar el servicio sin activar la casilla **Habilitar IntelliTrace para roles de .NET 4** .</span><span class="sxs-lookup"><span data-stu-id="6d9ee-182">Once you have verified that all errors have been corrected, you can deploy the service without checking the **Enable IntelliTrace for .NET 4 roles** check box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d9ee-183">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6d9ee-183">Next steps</span></span>
<span data-ttu-id="6d9ee-184">Vea más [artículos de solución de problemas](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) para servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="6d9ee-184">View more [troubleshooting articles](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="6d9ee-185">Para más información acerca de cómo solucionar los problemas de los roles de los servicios en la nube mediante el uso de datos de diagnóstico de equipos de PaaS de Azure, consulte la [serie de blogs de Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="6d9ee-185">To learn how to troubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, see [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
