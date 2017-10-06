---
title: "aaaEnable generador de perfiles de visión de aplicación de Azure en un recurso de servicios en la nube | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooset el analizador de hello en una aplicación ASP.NET hospedada por un recurso de servicios en la nube."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: b9ac3bca513bf4518f44780389a9f2945f6ccc98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-application-insights-profiler-on-an-azure-cloud-services-resource"></a><span data-ttu-id="4d683-103">Habilitación de Application Insights Profiler para un recurso de Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="4d683-103">Enable Application Insights Profiler on an Azure Cloud Services resource</span></span>

<span data-ttu-id="4d683-104">Este tutorial muestra cómo tooenable generador de perfiles de visión de aplicación de Azure en una aplicación ASP.NET hospedada por un recurso de servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="4d683-104">This walkthrough demonstrates how tooenable Azure Application Insights Profiler on an ASP.NET application hosted by an Azure Cloud Services resource.</span></span> <span data-ttu-id="4d683-105">ejemplos de Hello incluyen compatibilidad con máquinas virtuales de Azure y conjuntos de escalas de máquina virtual, Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4d683-105">hello examples include support for Azure Virtual Machines, virtual machine scale sets, and Azure Service Fabric.</span></span> <span data-ttu-id="4d683-106">todos los ejemplos de Hello se basan en plantillas que admiten el modelo de implementación de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4d683-106">hello examples all rely on templates that support hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="4d683-107">Para obtener más información sobre el modelo de implementación de hello, revise [Azure Resource Manager frente a la implementación clásica: comprender los modelos de implementación y Hola estado de los recursos](/azure-resource-manager/resource-manager-deployment-model).</span><span class="sxs-lookup"><span data-stu-id="4d683-107">For more information about hello deployment model, review [Azure Resource Manager vs. classic deployment: Understand deployment models and hello state of your resources](/azure-resource-manager/resource-manager-deployment-model).</span></span>

## <a name="overview"></a><span data-ttu-id="4d683-108">Información general</span><span class="sxs-lookup"><span data-stu-id="4d683-108">Overview</span></span>

<span data-ttu-id="4d683-109">Hola siguiente diagrama ilustra cómo funciona el generador de perfiles de Hola para recursos de servicios de nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="4d683-109">hello following diagram illustrates how hello profiler works for Azure Cloud Services resources.</span></span> <span data-ttu-id="4d683-110">Se usa una máquina virtual de Azure como ejemplo.</span><span class="sxs-lookup"><span data-stu-id="4d683-110">It uses an Azure virtual machine as an example.</span></span>

<span data-ttu-id="4d683-111">![Información general sobre](./media/enable-profiler-compute/overview.png) toocollect información para el procesamiento y la presentación en Hola portal de Azure, debe instalar el componente de agente de diagnóstico de Hola para los recursos de servicios en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d683-111">![Overview](./media/enable-profiler-compute/overview.png) toocollect information for processing and display on hello Azure portal, you must install hello Diagnostics Agent component for hello Azure Cloud Services resources.</span></span> <span data-ttu-id="4d683-112">Hello resto del tutorial de hello proporciona orientación sobre cómo tooinstall y configurar el agente de diagnóstico de hello tooenable el generador de perfiles de aplicación visión.</span><span class="sxs-lookup"><span data-stu-id="4d683-112">hello rest of hello walkthrough provides guidance on how tooinstall and configure hello Diagnostics Agent tooenable Application Insights Profiler.</span></span>

## <a name="prerequisites-for-hello-walkthrough"></a><span data-ttu-id="4d683-113">Requisitos previos de tutorial Hola</span><span class="sxs-lookup"><span data-stu-id="4d683-113">Prerequisites for hello walkthrough</span></span>

* <span data-ttu-id="4d683-114">Una plantilla de administrador de recursos de implementación que instala agentes de generador de perfiles de hello en hello las máquinas virtuales ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) o conjuntos de escala ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).</span><span class="sxs-lookup"><span data-stu-id="4d683-114">A deployment Resource Manager template that installs hello profiler agents on hello VMs ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) or scale sets ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).</span></span>

* <span data-ttu-id="4d683-115">Una instancia de Application Insights habilitada para la generación de perfiles.</span><span class="sxs-lookup"><span data-stu-id="4d683-115">An Application Insights instance enabled for profiling.</span></span> <span data-ttu-id="4d683-116">Para obtener instrucciones, consulte [Habilitar perfil de hello](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).</span><span class="sxs-lookup"><span data-stu-id="4d683-116">For instructions, see [Enable hello profile](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).</span></span>

* <span data-ttu-id="4d683-117">Recurso de servicios en la nube de destino de .NET framework 4.6.1 o posterior instalado en hello.</span><span class="sxs-lookup"><span data-stu-id="4d683-117">.NET Framework 4.6.1 or later installed on hello target Azure Cloud Services resource.</span></span>

## <a name="create-a-resource-group-in-your-azure-subscription"></a><span data-ttu-id="4d683-118">Creación de un grupo de recursos en la suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="4d683-118">Create a resource group in your Azure subscription</span></span>
<span data-ttu-id="4d683-119">Hola siguiente ejemplo muestra cómo agrupar toocreate un recurso mediante un script de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4d683-119">hello following example demonstrates how toocreate a resource group by using a PowerShell script:</span></span>

```
New-AzureRmResourceGroup -Name "Replace_With_Resource_Group_Name" -Location "Replace_With_Resource_Group_Location"
```

## <a name="create-an-application-insights-resource-in-hello-resource-group"></a><span data-ttu-id="4d683-120">Crear un recurso de Application Insights en grupo de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="4d683-120">Create an Application Insights resource in hello resource group</span></span>
<span data-ttu-id="4d683-121">En hello **Application Insights** hoja, especifique la información de hello para el recurso, como se muestra en este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4d683-121">On hello **Application Insights** blade, enter hello information for your resource, as shown in this example:</span></span> 

![Hoja Application Insights](./media/enable-profiler-compute/createai.png)

## <a name="apply-an-application-insights-instrumentation-key-in-hello-azure-resource-manager-template"></a><span data-ttu-id="4d683-123">Aplicar una clave de instrumentación de Application Insights en plantilla de Azure Resource Manager Hola</span><span class="sxs-lookup"><span data-stu-id="4d683-123">Apply an Application Insights instrumentation key in hello Azure Resource Manager template</span></span>

1. <span data-ttu-id="4d683-124">Si ha descargado todavía plantilla hello, descárguelo desde [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).</span><span class="sxs-lookup"><span data-stu-id="4d683-124">If you haven't downloaded hello template yet, download it from [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).</span></span>

2. <span data-ttu-id="4d683-125">Encontrar la clave de Application Insights Hola.</span><span class="sxs-lookup"><span data-stu-id="4d683-125">Find hello Application Insights key.</span></span>
   
   ![Ubicación de clave de Hola](./media/enable-profiler-compute/copyaikey.png)

3. <span data-ttu-id="4d683-127">Reemplace el valor de la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d683-127">Replace hello template value.</span></span>
   
   ![Valor reemplazado en la plantilla de Hola](./media/enable-profiler-compute/copyaikeytotemplate.png)

## <a name="create-an-azure-vm-toohost-hello-web-application"></a><span data-ttu-id="4d683-129">Crear una aplicación web de Azure VM toohost Hola</span><span class="sxs-lookup"><span data-stu-id="4d683-129">Create an Azure VM toohost hello web application</span></span>
1. <span data-ttu-id="4d683-130">Crear una contraseña de cadena segura toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="4d683-130">Create a secure string toosave hello password.</span></span>

   ```
   $password = ConvertTo-SecureString -String "Replace_With_Your_Password" -AsPlainText -Force
   ```

2. <span data-ttu-id="4d683-131">Implementar la plantilla de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4d683-131">Deploy hello Azure Resource Manager template.</span></span>

   <span data-ttu-id="4d683-132">Cambie el directorio de hello en la carpeta toohello de consola de PowerShell de Hola que contiene la plantilla de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="4d683-132">Change hello directory in hello PowerShell console toohello folder that contains your Resource Manager template.</span></span> <span data-ttu-id="4d683-133">plantilla de hello toodeploy, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="4d683-133">toodeploy hello template, run hello following command:</span></span>

   ```
   New-AzureRmResourceGroupDeployment -ResourceGroupName "Replace_With_Resource_Group_Name" -TemplateFile .\WindowsVirtualMachine.json -adminUsername "Replace_With_your_user_name" -adminPassword $password -dnsNameForPublicIP "Replace_WIth_your_DNS_Name" -Verbose
   ```

<span data-ttu-id="4d683-134">Una vez ejecutada correctamente la secuencia de comandos de hello, debería encontrar una máquina virtual denominada **MyWindowsVM** en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="4d683-134">After hello script runs successfully, you should find a VM named **MyWindowsVM** in your resource group.</span></span>

## <a name="configure-web-deploy-on-hello-vm"></a><span data-ttu-id="4d683-135">Configurar Web Deploy en hello VM</span><span class="sxs-lookup"><span data-stu-id="4d683-135">Configure Web Deploy on hello VM</span></span>
<span data-ttu-id="4d683-136">Asegúrese de que Web Deploy esté habilitado en la máquina virtual de forma que pueda publicar la aplicación web desde Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4d683-136">Make sure that Web Deploy is enabled on your VM so you can publish your web application from Visual Studio.</span></span>

<span data-ttu-id="4d683-137">tooinstall Web Deploy en una máquina virtual manualmente a través de WebPI, consulte [instalación y configuración de Web Deploy en IIS 8.0 o posterior](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later).</span><span class="sxs-lookup"><span data-stu-id="4d683-137">tooinstall Web Deploy on a VM manually via WebPI, see [Installing and Configuring Web Deploy on IIS 8.0 or Later](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later).</span></span> <span data-ttu-id="4d683-138">Para obtener un ejemplo de cómo tooautomate instalar Web Deploy mediante una plantilla de Azure Resource Manager, consulte [crear, configurar e implementar una tooan de aplicación web VM de Azure](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).</span><span class="sxs-lookup"><span data-stu-id="4d683-138">For an example of how tooautomate installing Web Deploy by using an Azure Resource Manager template, see [Create, configure, and deploy a web application tooan Azure VM](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).</span></span>

<span data-ttu-id="4d683-139">Si va a implementar una aplicación ASP.NET MVC, vaya tooServer Manager, seleccione **agregar Roles y características** > **servidor Web (IIS)** > **Web Server**  >  **Desarrollo de aplicaciones**y habilitar ASP.NET 4.5 en el servidor.</span><span class="sxs-lookup"><span data-stu-id="4d683-139">If you are deploying an ASP.NET MVC application, go tooServer Manager, select **Add Roles and Features** > **Web Server (IIS)** > **Web Server** > **Application Development**, and enable ASP.NET 4.5 on your server.</span></span>

![Adición de ASP.NET](./media/enable-profiler-compute/addaspnet45.png)

## <a name="install-hello-azure-application-insights-sdk-for-your-project"></a><span data-ttu-id="4d683-141">Instalar hello Azure Application Insights SDK para el proyecto</span><span class="sxs-lookup"><span data-stu-id="4d683-141">Install hello Azure Application Insights SDK for your project</span></span>
1. <span data-ttu-id="4d683-142">Abra la aplicación web ASP.NET en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4d683-142">Open your ASP.NET web application in Visual Studio.</span></span>

2. <span data-ttu-id="4d683-143">Haga clic en proyecto de Hola y seleccione **agregar** > **servicios conectados**.</span><span class="sxs-lookup"><span data-stu-id="4d683-143">Right-click hello project and select **Add** > **Connected Services**.</span></span>

3. <span data-ttu-id="4d683-144">Seleccione **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="4d683-144">Select **Application Insights**.</span></span>

4. <span data-ttu-id="4d683-145">Siga las instrucciones de hello en página Hola.</span><span class="sxs-lookup"><span data-stu-id="4d683-145">Follow hello instructions on hello page.</span></span> <span data-ttu-id="4d683-146">Seleccione el recurso de Application Insights de Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4d683-146">Select hello Application Insights resource that you created earlier.</span></span>

5. <span data-ttu-id="4d683-147">Seleccione hello **registrar** botón.</span><span class="sxs-lookup"><span data-stu-id="4d683-147">Select hello **Register** button.</span></span>


## <a name="publish-hello-project-tooan-azure-vm"></a><span data-ttu-id="4d683-148">Publicar Hola proyecto tooan máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="4d683-148">Publish hello project tooan Azure VM</span></span>
<span data-ttu-id="4d683-149">Hay toopublish de varias maneras de una máquina virtual de Azure tooan de aplicación.</span><span class="sxs-lookup"><span data-stu-id="4d683-149">There are several ways toopublish an application tooan Azure VM.</span></span> <span data-ttu-id="4d683-150">Una manera es toouse 2017 de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4d683-150">One way is toouse Visual Studio 2017.</span></span>

1. <span data-ttu-id="4d683-151">Haga clic en proyecto de Hola y seleccione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="4d683-151">Right-click hello project and select **Publish**.</span></span>

2. <span data-ttu-id="4d683-152">Seleccione **máquinas virtuales de Microsoft Azure** como Hola publicar destino y siga los pasos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d683-152">Select **Microsoft Azure Virtual Machines** as hello publish target and follow hello steps.</span></span>

   ![Publish-FromVS](./media/enable-profiler-compute/publishtoVM.png)

3. <span data-ttu-id="4d683-154">Ejecute una prueba de carga con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4d683-154">Run a load test against your application.</span></span> <span data-ttu-id="4d683-155">Debería ver los resultados en la página Web portal de hello Application Insights instancia.</span><span class="sxs-lookup"><span data-stu-id="4d683-155">You should see results on hello Application Insights instance portal webpage.</span></span>


## <a name="enable-hello-profiler"></a><span data-ttu-id="4d683-156">Habilitar el generador de perfiles de Hola</span><span class="sxs-lookup"><span data-stu-id="4d683-156">Enable hello profiler</span></span>
1. <span data-ttu-id="4d683-157">Vaya tooyour Application Insights **rendimiento** hoja y seleccione **configurar**.</span><span class="sxs-lookup"><span data-stu-id="4d683-157">Go tooyour Application Insights **Performance** blade and select **Configure**.</span></span>
   
   ![Icono Configurar](./media/enable-profiler-compute/enableprofiler1.png)
 
2. <span data-ttu-id="4d683-159">Seleccione **Habilitar el generador de perfiles**.</span><span class="sxs-lookup"><span data-stu-id="4d683-159">Select **Enable Profiler**.</span></span>
   
   ![Icono Habilitar el generador de perfiles](./media/enable-profiler-compute/enableprofiler2.png)

## <a name="add-a-performance-test-tooyour-application"></a><span data-ttu-id="4d683-161">Agregar una aplicación de tooyour de prueba de rendimiento</span><span class="sxs-lookup"><span data-stu-id="4d683-161">Add a performance test tooyour application</span></span>
<span data-ttu-id="4d683-162">Para poder recopilar algunos toobe de datos de ejemplo mostrado en el generador de perfiles de aplicación visión, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4d683-162">Follow these steps so we can collect some sample data toobe displayed in Application Insights Profiler:</span></span>

1. <span data-ttu-id="4d683-163">Examinar los recursos de Application Insights toohello que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4d683-163">Browse toohello Application Insights resource that you created earlier.</span></span> 

2. <span data-ttu-id="4d683-164">Vaya toohello **disponibilidad** hoja y agregue una prueba de rendimiento que envía la dirección URL de la aplicación de web solicitudes tooyour.</span><span class="sxs-lookup"><span data-stu-id="4d683-164">Go toohello **Availability** blade and add a performance test that sends web requests tooyour application URL.</span></span> 

   ![Adición de una prueba de rendimiento](./media/enable-profiler-compute/AvailabilityTest.png)

## <a name="view-your-performance-data"></a><span data-ttu-id="4d683-166">Visualización de los datos de rendimiento</span><span class="sxs-lookup"><span data-stu-id="4d683-166">View your performance data</span></span>

1. <span data-ttu-id="4d683-167">Espere 10 y 15 minutos para toocollect del generador de perfiles de Hola y analizar datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d683-167">Wait 10-15 minutes for hello profiler toocollect and analyze hello data.</span></span> 

2. <span data-ttu-id="4d683-168">Vaya toohello **rendimiento** hoja en el recurso de Application Insights y la vista de rendimiento de la aplicación cuando está bajo carga.</span><span class="sxs-lookup"><span data-stu-id="4d683-168">Go toohello **Performance** blade in your Application Insights resource and view how your application is performing when it's under load.</span></span>

   ![Visualización del rendimiento](./media/enable-profiler-compute/aiperformance.png)

3. <span data-ttu-id="4d683-170">Icono de SELECT hello en **ejemplos** tooopen hello **vista seguimiento** hoja.</span><span class="sxs-lookup"><span data-stu-id="4d683-170">Select hello icon under **Examples** tooopen hello **Trace View** blade.</span></span>

   ![Abrir la hoja de la vista de seguimiento de Hola](./media/enable-profiler-compute/traceview.png)


## <a name="work-with-an-existing-template"></a><span data-ttu-id="4d683-172">Uso de una plantilla existente</span><span class="sxs-lookup"><span data-stu-id="4d683-172">Work with an existing template</span></span>

1. <span data-ttu-id="4d683-173">Busque la declaración del recurso Hola diagnósticos de Azure en la plantilla de implementación.</span><span class="sxs-lookup"><span data-stu-id="4d683-173">Locate hello Azure Diagnostics resource declaration in your deployment template.</span></span>
   
   <span data-ttu-id="4d683-174">Si no tiene una declaración, puede crear uno que es similar a la declaración de hello en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d683-174">If you don't have a declaration, you can create one that resembles hello declaration in hello following example.</span></span> <span data-ttu-id="4d683-175">Puede actualizar la plantilla de Hola de hello [sitio Web del explorador de recursos de Azure](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4d683-175">You can update hello template from hello [Azure Resource Explorer website](https://resources.azure.com).</span></span>

2. <span data-ttu-id="4d683-176">Publicador de cambios de Hola de `Microsoft.Azure.Diagnostics` demasiado`AIP.Diagnostics.Test`.</span><span class="sxs-lookup"><span data-stu-id="4d683-176">Change hello publisher from `Microsoft.Azure.Diagnostics` too`AIP.Diagnostics.Test`.</span></span>

3. <span data-ttu-id="4d683-177">Para `typeHandlerVersion`, utilice `0.0`.</span><span class="sxs-lookup"><span data-stu-id="4d683-177">For `typeHandlerVersion`, use `0.0`.</span></span>

4. <span data-ttu-id="4d683-178">Asegúrese de que `autoUpgradeMinorVersion` se establece demasiado`true`.</span><span class="sxs-lookup"><span data-stu-id="4d683-178">Make sure that `autoUpgradeMinorVersion` is set too`true`.</span></span>

5. <span data-ttu-id="4d683-179">Agregar nueva hello `ApplicationInsightsProfiler` instancia receptor Hola `WadCfg` objeto de configuración, tal y como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="4d683-179">Add hello new `ApplicationInsightsProfiler` sink instance in hello `WadCfg` settings object, as shown in hello following example:</span></span>

```
"resources": [
        {
          "type": "extensions",
          "name": "Microsoft.Insights.VMDiagnosticsSettings",
          "apiVersion": "2016-03-30",
          "properties": {
            "publisher": "AIP.Diagnostics.Test",
            "type": "IaaSDiagnostics",
            "typeHandlerVersion": "0.0",
            "autoUpgradeMinorVersion": true,
            "settings": {
              "WadCfg": {
                "SinksConfig": {
                  "Sink": [
                    {
                      "name": "Give a descriptive short name. E.g.: MyApplicationInsightsProfilerSink",
                      "ApplicationInsightsProfiler": "Enter hello Application Insights instance instrumentation key guid here"
                    }
                  ]
                },
                "DiagnosticMonitorConfiguration": {
                    ...
                }
                ...
              }
              ...
            }
            ...
          }
          ...
]
```

## <a name="enable-hello-profiler-on-virtual-machine-scale-sets"></a><span data-ttu-id="4d683-180">Habilitar el generador de perfiles de hello en conjuntos de escalas de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="4d683-180">Enable hello profiler on virtual machine scale sets</span></span>
<span data-ttu-id="4d683-181">toosee cómo tooenable Hola profiler, descargar hello [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) plantilla.</span><span class="sxs-lookup"><span data-stu-id="4d683-181">toosee how tooenable hello profiler, download hello [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) template.</span></span> <span data-ttu-id="4d683-182">Hola mismos cambios en un recurso de extensión de diagnóstico de máquina virtual plantilla toohello para el conjunto de escalas de máquina virtual de Hola se aplican.</span><span class="sxs-lookup"><span data-stu-id="4d683-182">Apply hello same changes in a VM template toohello diagnostics extension resource for hello virtual machine scale set.</span></span>

<span data-ttu-id="4d683-183">Asegúrese de que cada instancia en conjunto de escalas de Hola tiene toohello de acceso a internet.</span><span class="sxs-lookup"><span data-stu-id="4d683-183">Make sure that each instance in hello scale set has access toohello internet.</span></span> <span data-ttu-id="4d683-184">Hola generador de perfiles de agente, a continuación, puede enviar muestras de hello recopilan tooApplication visión para la presentación y análisis.</span><span class="sxs-lookup"><span data-stu-id="4d683-184">hello Profiler Agent can then send hello collected samples tooApplication Insights for display and analysis.</span></span>

## <a name="enable-hello-profiler-on-service-fabric-applications"></a><span data-ttu-id="4d683-185">Habilitar el generador de perfiles de hello en aplicaciones de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4d683-185">Enable hello profiler on Service Fabric applications</span></span>
1. <span data-ttu-id="4d683-186">Hola aprovisionar Service Fabric clúster toohave hello Azure extensión de diagnósticos que instala Hola generador de perfiles de agente.</span><span class="sxs-lookup"><span data-stu-id="4d683-186">Provision hello Service Fabric cluster toohave hello Azure Diagnostics extension that installs hello Profiler Agent.</span></span>

2. <span data-ttu-id="4d683-187">Instalar Hola Application Insights SDK en el proyecto de Hola y configurar clave de Application Insights Hola.</span><span class="sxs-lookup"><span data-stu-id="4d683-187">Install hello Application Insights SDK in hello project and configure hello Application Insights key.</span></span>

3. <span data-ttu-id="4d683-188">Agregar telemetría de tooinstrument de código de aplicación.</span><span class="sxs-lookup"><span data-stu-id="4d683-188">Add application code tooinstrument telemetry.</span></span>

### <a name="provision-hello-service-fabric-cluster-toohave-hello-azure-diagnostics-extension-that-installs-hello-profiler-agent"></a><span data-ttu-id="4d683-189">Aprovisionar Hola Service Fabric clúster toohave Hola extensión de diagnósticos de Azure que instala Hola generador de perfiles de agente</span><span class="sxs-lookup"><span data-stu-id="4d683-189">Provision hello Service Fabric cluster toohave hello Azure Diagnostics extension that installs hello Profiler Agent</span></span>
<span data-ttu-id="4d683-190">Un clúster de Service Fabric puede ser seguro o no seguro.</span><span class="sxs-lookup"><span data-stu-id="4d683-190">A Service Fabric cluster can be secure or non-secure.</span></span> <span data-ttu-id="4d683-191">Puede establecer una toobe de clúster de puerta de enlace no seguras por lo que no requiere un certificado para el acceso.</span><span class="sxs-lookup"><span data-stu-id="4d683-191">You can set one gateway cluster toobe non-secure so it doesn't require a certificate for access.</span></span> <span data-ttu-id="4d683-192">Los clústeres que hospedan lógica y datos empresariales deben ser seguros.</span><span class="sxs-lookup"><span data-stu-id="4d683-192">Clusters that host business logic and data should be secure.</span></span> <span data-ttu-id="4d683-193">Puede habilitar el generador de perfiles de hello en clústeres de Service Fabric seguros y no seguras.</span><span class="sxs-lookup"><span data-stu-id="4d683-193">You can enable hello profiler on both secure and non-secure Service Fabric clusters.</span></span> <span data-ttu-id="4d683-194">En este tutorial usa un clúster no seguras como un ejemplo tooexplain los cambios que son necesarios tooenable Hola profiler.</span><span class="sxs-lookup"><span data-stu-id="4d683-194">This walkthrough uses a non-secure cluster as an example tooexplain what changes are required tooenable hello profiler.</span></span> <span data-ttu-id="4d683-195">Puede aprovisionar un clúster segura Hola igual.</span><span class="sxs-lookup"><span data-stu-id="4d683-195">You can provision a secure cluster in hello same way.</span></span>

1. <span data-ttu-id="4d683-196">Descargue [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json).</span><span class="sxs-lookup"><span data-stu-id="4d683-196">Download [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json).</span></span> <span data-ttu-id="4d683-197">Al igual que hizo con las máquinas virtuales y los conjuntos de escalado de máquinas virtuales, sustituya `Application_Insights_Key` por la clave de Application Insights:</span><span class="sxs-lookup"><span data-stu-id="4d683-197">As you did for VMs and virtual machine scale sets, replace `Application_Insights_Key` with your Application Insights key:</span></span>

   ```
   "publisher": "AIP.Diagnostics.Test",
                 "settings": {
                   "WadCfg": {
                     "SinksConfig": {
                       "Sink": [
                         {
                           "name": "MyApplicationInsightsProfilerSinkVMSS",
                           "ApplicationInsightsProfiler": "[Application_Insights_Key]"
                         }
                       ]
                     },
   ```

2. <span data-ttu-id="4d683-198">Implementar la plantilla de hello mediante un script de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4d683-198">Deploy hello template by using a PowerShell script:</span></span>

   ```
   Login-AzureRmAccount
   New-AzureRmResourceGroup -Name [Your_Resource_Group_Name] -Location [Your_Resource_Group_Location] -Verbose -Force
   New-AzureRmResourceGroupDeployment -Name [Choose_An_Arbitrary_Name] -ResourceGroupName [Your_Resource_Group_Name] -TemplateFile [Path_To_Your_Template]

   ```

### <a name="install-hello-application-insights-sdk-in-hello-project-and-configure-hello-application-insights-key"></a><span data-ttu-id="4d683-199">Instalar Hola Application Insights SDK en proyecto de Hola y configurar la clave de Application Insights Hola</span><span class="sxs-lookup"><span data-stu-id="4d683-199">Install hello Application Insights SDK in hello project and configure hello Application Insights key</span></span>
<span data-ttu-id="4d683-200">Instalar Hola Application Insights SDK desde hello [paquete NuGet](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span><span class="sxs-lookup"><span data-stu-id="4d683-200">Install hello Application Insights SDK from hello [NuGet package](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span></span> <span data-ttu-id="4d683-201">Asegúrese de instalar una versión estable, la 2.3 o posterior.</span><span class="sxs-lookup"><span data-stu-id="4d683-201">Make sure that you install a stable version, 2.3 or later.</span></span> 

<span data-ttu-id="4d683-202">Para más información sobre la configuración de Application Insights en los proyectos, consulte [Using Service Fabric with Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md) (Uso de Service Fabric con Application Insights).</span><span class="sxs-lookup"><span data-stu-id="4d683-202">For information about configuring Application Insights in your projects, see [Using Service Fabric with Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md).</span></span>

### <a name="add-application-code-tooinstrument-telemetry"></a><span data-ttu-id="4d683-203">Agregar telemetría de tooinstrument de código de aplicación</span><span class="sxs-lookup"><span data-stu-id="4d683-203">Add application code tooinstrument telemetry</span></span>
1. <span data-ttu-id="4d683-204">Para cualquier fragmento de código que desea que tooinstrument, agregar un elemento using instrucción alrededor de ella.</span><span class="sxs-lookup"><span data-stu-id="4d683-204">For any piece of code that you want tooinstrument, add a using statement around it.</span></span> 

   <span data-ttu-id="4d683-205">En el siguiente ejemplo de Hola Hola `RunAsync` método es hacer algún trabajo y Hola `telemetryClient` clase captura telemetría Hola después de iniciarse.</span><span class="sxs-lookup"><span data-stu-id="4d683-205">In hello following  example, hello `RunAsync` method is doing some work, and hello `telemetryClient` class captures hello telemetry after it starts.</span></span> <span data-ttu-id="4d683-206">evento de Hello requiere un nombre único a través de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="4d683-206">hello event needs a unique name across hello application.</span></span>

   ```
   protected override async Task RunAsync(CancellationToken cancellationToken)
       {
           // TODO: Replace hello following sample code with your own logic
           //       or remove this RunAsync override if it's not needed in your service.

           while (true)
           {
               using( var operation = telemetryClient.StartOperation<RequestTelemetry>("[Insert_Event_Unique_Name]"))
               {
                   cancellationToken.ThrowIfCancellationRequested();

                   ++this.iterations;

                   ServiceEventSource.Current.ServiceMessage(this.Context, "Working-{0}", this.iterations);

                   await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
               }

           }
       }
   ```

2. <span data-ttu-id="4d683-207">Implementar el clúster de Service Fabric toohello de aplicación.</span><span class="sxs-lookup"><span data-stu-id="4d683-207">Deploy your application toohello Service Fabric cluster.</span></span> <span data-ttu-id="4d683-208">Espere 10 minutos para toorun de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="4d683-208">Wait for hello app toorun for 10 minutes.</span></span> <span data-ttu-id="4d683-209">Para obtener un mejor efecto, puede ejecutar una prueba de carga en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="4d683-209">For better effect, you can run a load test on hello app.</span></span> <span data-ttu-id="4d683-210">Del portal de Application Insights vaya toohello **rendimiento** hoja y se deberían ver ejemplos de seguimientos de generación de perfiles.</span><span class="sxs-lookup"><span data-stu-id="4d683-210">Go toohello Application Insights portal's **Performance** blade, and you should see examples of profiling traces appear.</span></span>

<!---
Commenting out these sections for now
## Enable hello Profiler on Cloud Services applications
[TODO]
## Enable hello Profiler on classic Azure Virtual Machines
[TODO]
## Enable hello Profiler on on-premise servers
[TODO]
--->

## <a name="next-steps"></a><span data-ttu-id="4d683-211">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4d683-211">Next steps</span></span>

- <span data-ttu-id="4d683-212">Encuentre ayuda con los problemas de Profiler en la sección de [solución de problemas](app-insights-profiler.md#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="4d683-212">Find help with troubleshooting profiler issues in [Profiler troubleshooting](app-insights-profiler.md#troubleshooting).</span></span>

- <span data-ttu-id="4d683-213">Obtenga más información sobre el analizador de hello en [el generador de perfiles de aplicación visión](app-insights-profiler.md).</span><span class="sxs-lookup"><span data-stu-id="4d683-213">Read more about hello profiler in [Application Insights Profiler](app-insights-profiler.md).</span></span>
