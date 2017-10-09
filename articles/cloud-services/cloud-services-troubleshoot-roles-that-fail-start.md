---
title: roles de aaaTroubleshoot que no se toostart | Documentos de Microsoft
description: "A continuación figuran algunas causas habituales por qué un rol de servicio de nube puede producir un error toostart. También se proporcionan soluciones problemas de toothese."
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
ms.openlocfilehash: e2fbecb08a10984add79dfc74e73de6869bb314f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-roles-that-fail-toostart"></a><span data-ttu-id="f9e5e-104">Solucionar problemas de los roles de servicio en la nube que no se toostart</span><span class="sxs-lookup"><span data-stu-id="f9e5e-104">Troubleshoot Cloud Service roles that fail toostart</span></span>
<span data-ttu-id="f9e5e-105">Estos son algunos problemas comunes y los roles de servicios en la nube de tooAzure relacionados de soluciones que no se toostart.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-105">Here are some common problems and solutions related tooAzure Cloud Services roles that fail toostart.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-dlls-or-dependencies"></a><span data-ttu-id="f9e5e-106">DLL o dependencias que faltan</span><span class="sxs-lookup"><span data-stu-id="f9e5e-106">Missing DLLs or dependencies</span></span>
<span data-ttu-id="f9e5e-107">Tanto que los roles no respondan como que alternen entre los estados **Inicializando**, **Ocupado** y **Deteniendo** puede deberse a que faltan DLL o ensamblados.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-107">Unresponsive roles and roles that are cycling between **Initializing**, **Busy**, and **Stopping** states can be caused by missing DLLs or assemblies.</span></span>

<span data-ttu-id="f9e5e-108">Estos son los síntomas de que faltan DLL o ensamblados:</span><span class="sxs-lookup"><span data-stu-id="f9e5e-108">Symptoms of missing DLLs or assemblies can be:</span></span>

* <span data-ttu-id="f9e5e-109">Una instancia de rol alterna entre los estados **Inicializando**, **Ocupado** y **Deteniendo**.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-109">Your role instance is cycling through **Initializing**, **Busy**, and **Stopping** states.</span></span>
* <span data-ttu-id="f9e5e-110">La instancia de rol se movió demasiado**listo** pero si navega aplicación web de tooyour, no aparece la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-110">Your role instance has moved too**Ready** but if you navigate tooyour web application, hello page does not appear.</span></span>

<span data-ttu-id="f9e5e-111">Hay varios métodos recomendados para investigar estos problemas.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-111">There are several recommended methods for investigating these issues.</span></span>

## <a name="diagnose-missing-dll-issues-in-a-web-role"></a><span data-ttu-id="f9e5e-112">Diagnóstico del problema de DLL que faltan en un rol web</span><span class="sxs-lookup"><span data-stu-id="f9e5e-112">Diagnose missing DLL issues in a web role</span></span>
<span data-ttu-id="f9e5e-113">Cuando vaya sitio Web de tooa que se implementa en un rol web y Explorador de hello muestra un servidor error similar toohello después, puede indicar que un archivo DLL es que faltan.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-113">When you navigate tooa website that is deployed in a web role, and hello browser displays a server error similar toohello following, it may indicate that a DLL is missing.</span></span>

![Error del servidor en la aplicación '/'](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503388.png)

## <a name="diagnose-issues-by-turning-off-custom-errors"></a><span data-ttu-id="f9e5e-115">Diagnóstico de problemas mediante la desactivación de errores personalizados</span><span class="sxs-lookup"><span data-stu-id="f9e5e-115">Diagnose issues by turning off custom errors</span></span>
<span data-ttu-id="f9e5e-116">Información de error más completa puede verse mediante la configuración de web.config de Hola para hello web rol tooset Hola errores personalizados modo tooOff y volver a implementar el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-116">More complete error information can be viewed by configuring hello web.config for hello web role tooset hello custom error mode tooOff and redeploying hello service.</span></span>

<span data-ttu-id="f9e5e-117">tooview complete más errores sin utilizar Escritorio remoto:</span><span class="sxs-lookup"><span data-stu-id="f9e5e-117">tooview more complete errors without using Remote Desktop:</span></span>

1. <span data-ttu-id="f9e5e-118">Abra la solución de hello en Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-118">Open hello solution in Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="f9e5e-119">Hola **el Explorador de soluciones**, busque el archivo web.config de hello y ábralo.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-119">In hello **Solution Explorer**, locate hello web.config file and open it.</span></span>
3. <span data-ttu-id="f9e5e-120">En el archivo web.config de hello, busque la sección system.web de Hola y agregue Hola después de línea:</span><span class="sxs-lookup"><span data-stu-id="f9e5e-120">In hello web.config file, locate hello system.web section and add hello following line:</span></span>

    ```xml
    <customErrors mode="Off" />
    ```
4. <span data-ttu-id="f9e5e-121">Guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-121">Save hello file.</span></span>
5. <span data-ttu-id="f9e5e-122">Volver a empaquetar e implementar el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-122">Repackage and redeploy hello service.</span></span>

<span data-ttu-id="f9e5e-123">Una vez que se vuelve a implementar el servicio de hello, verá un mensaje de error con el nombre de Hola de hello falta el ensamblado o una DLL.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-123">Once hello service is redeployed, you will see an error message with hello name of hello missing assembly or DLL.</span></span>

## <a name="diagnose-issues-by-viewing-hello-error-remotely"></a><span data-ttu-id="f9e5e-124">Diagnosticar problemas comprobando error Hola de forma remota</span><span class="sxs-lookup"><span data-stu-id="f9e5e-124">Diagnose issues by viewing hello error remotely</span></span>
<span data-ttu-id="f9e5e-125">Puede usar Escritorio remoto tooaccess Hola rol y ver información de error más completa de forma remota.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-125">You can use Remote Desktop tooaccess hello role and view more complete error information remotely.</span></span> <span data-ttu-id="f9e5e-126">Use Hola siguientes pasos le indican errores de hello tooview mediante Escritorio remoto:</span><span class="sxs-lookup"><span data-stu-id="f9e5e-126">Use hello following steps tooview hello errors by using Remote Desktop:</span></span>

1. <span data-ttu-id="f9e5e-127">Asegúrese de que está instalado el SDK 1.3 de Azure, o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-127">Ensure that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="f9e5e-128">Durante la implementación de Hola de solución de hello mediante Visual Studio, elija demasiado "Conexiones a Escritorio remoto configurar …".</span><span class="sxs-lookup"><span data-stu-id="f9e5e-128">During hello deployment of hello solution by using Visual Studio, choose too“Configure Remote Desktop connections…”.</span></span> <span data-ttu-id="f9e5e-129">Para obtener más información sobre la configuración de conexión a Escritorio remoto hello, consulte [usar Escritorio remoto con Roles de Azure](../vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="f9e5e-129">For more information on configuring hello Remote Desktop connection, see [Using Remote Desktop with Azure Roles](../vs-azure-tools-remote-desktop-roles.md).</span></span>
3. <span data-ttu-id="f9e5e-130">En hello clásico portal de Microsoft Azure, una vez que la instancia de hello muestra un estado de **listo**, haga clic en una de las instancias de rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-130">In hello Microsoft Azure classic portal, once hello instance shows a status of **Ready**, click one of hello role instances.</span></span>
4. <span data-ttu-id="f9e5e-131">Haga clic en hello **conectar** icono Hola **acceso remoto** área no cliente de la cinta de opciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-131">Click hello **Connect** icon in hello **Remote Access** area of hello ribbon.</span></span>
5. <span data-ttu-id="f9e5e-132">Inicie sesión en la máquina virtual de toohello mediante credenciales de Hola que se especificaron durante la configuración de escritorio remoto de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-132">Sign in toohello virtual machine by using hello credentials that were specified during hello Remote Desktop configuration.</span></span>
6. <span data-ttu-id="f9e5e-133">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-133">Open a command window.</span></span>
7. <span data-ttu-id="f9e5e-134">Escriba `IPconfig`.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-134">Type `IPconfig`.</span></span>
8. <span data-ttu-id="f9e5e-135">Anote el valor de la dirección IPV4 de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-135">Note hello IPV4 Address value.</span></span>
9. <span data-ttu-id="f9e5e-136">Abra Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-136">Open Internet Explorer.</span></span>
10. <span data-ttu-id="f9e5e-137">Escriba la dirección de Hola y el nombre de Hola de aplicación web de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-137">Type hello address and hello name of hello web application.</span></span> <span data-ttu-id="f9e5e-138">Por ejemplo: `http://<IPV4 Address>/default.aspx`.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-138">For example, `http://<IPV4 Address>/default.aspx`.</span></span>

<span data-ttu-id="f9e5e-139">Navegar por toohello sitio Web devolverá ahora más explícitos mensajes de error:</span><span class="sxs-lookup"><span data-stu-id="f9e5e-139">Navigating toohello website will now return more explicit error messages:</span></span>

* <span data-ttu-id="f9e5e-140">Error del servidor en la aplicación '/'</span><span class="sxs-lookup"><span data-stu-id="f9e5e-140">Server Error in '/' Application.</span></span>
* <span data-ttu-id="f9e5e-141">Descripción: Se produjo una excepción no controlada durante la ejecución de saludo de solicitud web actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-141">Description: An unhandled exception occurred during hello execution of hello current web request.</span></span> <span data-ttu-id="f9e5e-142">Revise el seguimiento de la pila de Hola para obtener más información sobre el error de Hola y dónde se originó en el código de hello.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-142">Please review hello stack trace for more information about hello error and where it originated in hello code.</span></span>
* <span data-ttu-id="f9e5e-143">Detalles de la excepción: System.IO.FIleNotFoundException: No se puede cargar el archivo o ensamblado ‘Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35’ ni una de sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-143">Exception Details: System.IO.FIleNotFoundException: Could not load file or assembly ‘Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35’ or one of its dependencies.</span></span> <span data-ttu-id="f9e5e-144">sistema de Hello no encuentra el archivo hello especificado.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-144">hello system cannot find hello file specified.</span></span>

<span data-ttu-id="f9e5e-145">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f9e5e-145">For example:</span></span>

![Error explícito del servidor en la aplicación '/'](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503389.png)

## <a name="diagnose-issues-by-using-hello-compute-emulator"></a><span data-ttu-id="f9e5e-147">Diagnosticar problemas con el emulador de proceso de Hola</span><span class="sxs-lookup"><span data-stu-id="f9e5e-147">Diagnose issues by using hello compute emulator</span></span>
<span data-ttu-id="f9e5e-148">Puede usar Hola Microsoft Azure compute emulator toodiagnose y solucionar los problemas de falta de dependencias y errores en web.config.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-148">You can use hello Microsoft Azure compute emulator toodiagnose and troubleshoot issues of missing dependencies and web.config errors.</span></span>

<span data-ttu-id="f9e5e-149">Para obtener unos mejores resultados con este método de diagnóstico, debe usar un equipo o máquina virtual que tenga una instalación limpia de Windows.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-149">For best results in using this method of diagnosis, you should use a computer or virtual machine that has a clean installation of Windows.</span></span> <span data-ttu-id="f9e5e-150">toobest simular Hola entorno de Azure, use Windows Server 2008 R2 x64.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-150">toobest simulate hello Azure environment, use Windows Server 2008 R2 x64.</span></span>

1. <span data-ttu-id="f9e5e-151">Instalar la versión independiente de Hola de hello [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="f9e5e-151">Install hello standalone version of hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="f9e5e-152">En el equipo de desarrollo de hello, compile el proyecto de servicio de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-152">On hello development machine, build hello cloud service project.</span></span>
3. <span data-ttu-id="f9e5e-153">En el Explorador de Windows, desplazarse por las carpetas de toohello bin\debug del proyecto de servicio de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-153">In Windows Explorer, navigate toohello bin\debug folder of hello cloud service project.</span></span>
4. <span data-ttu-id="f9e5e-154">Copie la carpeta de .csx de Hola y el equipo de toohello de archivo de .cscfg que utilizas problemas de hello toodebug.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-154">Copy hello .csx folder and .cscfg file toohello computer that you are using toodebug hello issues.</span></span>
5. <span data-ttu-id="f9e5e-155">En hello limpieza máquina, abra una ventana de símbolo del sistema de SDK de Azure y un tipo `csrun.exe /devstore:start`.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-155">On hello clean machine, open an Azure SDK Command Prompt window and type `csrun.exe /devstore:start`.</span></span>
6. <span data-ttu-id="f9e5e-156">En hello símbolo del sistema, escriba `run csrun <path too.csx folder> <path too.cscfg file> /launchBrowser`.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-156">At hello command prompt, type `run csrun <path too.csx folder> <path too.cscfg file> /launchBrowser`.</span></span>
7. <span data-ttu-id="f9e5e-157">Cuando se inicia el rol de hello, verá información detallada del error en Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-157">When hello role starts, you will see detailed error information in Internet Explorer.</span></span> <span data-ttu-id="f9e5e-158">También puede usar herramientas para solucionar problemas de Windows estándares toofurther diagnosticar el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-158">You can also use standard Windows troubleshooting tools toofurther diagnose hello problem.</span></span>

## <a name="diagnose-issues-by-using-intellitrace"></a><span data-ttu-id="f9e5e-159">Diagnóstico de problemas mediante IntelliTrace</span><span class="sxs-lookup"><span data-stu-id="f9e5e-159">Diagnose issues by using IntelliTrace</span></span>
<span data-ttu-id="f9e5e-160">Para los roles web y de trabajo que usan .NET Framework 4, puede usar [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), que está disponible en Microsoft Visual Studio Enterprise.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-160">For worker and web roles that use .NET Framework 4, you can use [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), which is available in Microsoft Visual Studio Enterprise.</span></span>

<span data-ttu-id="f9e5e-161">Siga estos servicios de hello toodeploy pasos con IntelliTrace habilitado:</span><span class="sxs-lookup"><span data-stu-id="f9e5e-161">Follow these steps toodeploy hello service with IntelliTrace enabled:</span></span>

1. <span data-ttu-id="f9e5e-162">Confirme que está instalado el SDK 1.3 de Azure, o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-162">Confirm that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="f9e5e-163">Implementar soluciones de hello mediante Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-163">Deploy hello solution by using Visual Studio.</span></span> <span data-ttu-id="f9e5e-164">Durante la implementación, compruebe hello **Habilitar IntelliTrace para roles de .NET 4** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-164">During deployment, check hello **Enable IntelliTrace for .NET 4 roles** check box.</span></span>
3. <span data-ttu-id="f9e5e-165">Una vez que se inicia la instancia de hello, abra hello **Explorador de servidores**.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-165">Once hello instance starts, open hello **Server Explorer**.</span></span>
4. <span data-ttu-id="f9e5e-166">Expanda hello **Azure\\servicios en la nube** nodo y busque la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-166">Expand hello **Azure\\Cloud Services** node and locate hello deployment.</span></span>
5. <span data-ttu-id="f9e5e-167">Expandir la implementación de hello hasta que vea instancias de rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-167">Expand hello deployment until you see hello role instances.</span></span> <span data-ttu-id="f9e5e-168">Haga doble clic en una de las instancias de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-168">Right-click on one of hello instances.</span></span>
6. <span data-ttu-id="f9e5e-169">Elija **Ver registros de IntelliTrace**.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-169">Choose **View IntelliTrace logs**.</span></span> <span data-ttu-id="f9e5e-170">Hola **resumen de IntelliTrace** se abrirá.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-170">hello **IntelliTrace Summary** will open.</span></span>
7. <span data-ttu-id="f9e5e-171">Busque la sección de excepciones de Hola de hello resumen.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-171">Locate hello exceptions section of hello summary.</span></span> <span data-ttu-id="f9e5e-172">Si hay excepciones, se denominará sección hello **datos de excepción**.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-172">If there are exceptions, hello section will be labeled **Exception Data**.</span></span>
8. <span data-ttu-id="f9e5e-173">Expanda hello **datos de excepción** y busque **System.IO.FileNotFoundException** siguiente toohello similar de errores:</span><span class="sxs-lookup"><span data-stu-id="f9e5e-173">Expand hello **Exception Data** and look for **System.IO.FileNotFoundException** errors similar toohello following:</span></span>

![Datos de excepción, faltan archivo o ensamblado](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503390.png)

## <a name="address-missing-dlls-and-assemblies"></a><span data-ttu-id="f9e5e-175">Tratamiento de archivos DLL y ensamblados que faltan</span><span class="sxs-lookup"><span data-stu-id="f9e5e-175">Address missing DLLs and assemblies</span></span>
<span data-ttu-id="f9e5e-176">tooaddress falta errores de DLL y ensamblados, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="f9e5e-176">tooaddress missing DLL and assembly errors, follow these steps:</span></span>

1. <span data-ttu-id="f9e5e-177">Abra la solución de hello en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-177">Open hello solution in Visual Studio.</span></span>
2. <span data-ttu-id="f9e5e-178">En **el Explorador de soluciones**, abra hello **referencias** carpeta.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-178">In **Solution Explorer**, open hello **References** folder.</span></span>
3. <span data-ttu-id="f9e5e-179">Haga clic en ensamblado hello identificado en error Hola.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-179">Click hello assembly identified in hello error.</span></span>
4. <span data-ttu-id="f9e5e-180">Hola **propiedades** panel, busque **propiedad Copy Local** y establezca el valor de hello demasiado**True**.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-180">In hello **Properties** pane, locate **Copy Local property** and set hello value too**True**.</span></span>
5. <span data-ttu-id="f9e5e-181">Vuelva a implementar el servicio de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-181">Redeploy hello cloud service.</span></span>

<span data-ttu-id="f9e5e-182">Una vez haya comprobado que se han solucionado todos los errores, puede implementar el servicio de hello sin comprobar hello **Habilitar IntelliTrace para roles de .NET 4** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-182">Once you have verified that all errors have been corrected, you can deploy hello service without checking hello **Enable IntelliTrace for .NET 4 roles** check box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9e5e-183">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f9e5e-183">Next steps</span></span>
<span data-ttu-id="f9e5e-184">Vea más [artículos de solución de problemas](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) para servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="f9e5e-184">View more [troubleshooting articles](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="f9e5e-185">toolearn cómo emite tootroubleshoot rol de servicio de nube mediante el uso de datos de diagnóstico del equipo de PaaS de Azure, consulte [serie de blogs de Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="f9e5e-185">toolearn how tootroubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, see [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
