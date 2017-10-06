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
# <a name="enable-application-insights-profiler-on-an-azure-cloud-services-resource"></a>Habilitación de Application Insights Profiler para un recurso de Azure Cloud Services

Este tutorial muestra cómo tooenable generador de perfiles de visión de aplicación de Azure en una aplicación ASP.NET hospedada por un recurso de servicios en la nube. ejemplos de Hello incluyen compatibilidad con máquinas virtuales de Azure y conjuntos de escalas de máquina virtual, Azure Service Fabric. todos los ejemplos de Hello se basan en plantillas que admiten el modelo de implementación de hello Azure Resource Manager. Para obtener más información sobre el modelo de implementación de hello, revise [Azure Resource Manager frente a la implementación clásica: comprender los modelos de implementación y Hola estado de los recursos](/azure-resource-manager/resource-manager-deployment-model).

## <a name="overview"></a>Información general

Hola siguiente diagrama ilustra cómo funciona el generador de perfiles de Hola para recursos de servicios de nube de Azure. Se usa una máquina virtual de Azure como ejemplo.

![Información general sobre](./media/enable-profiler-compute/overview.png) toocollect información para el procesamiento y la presentación en Hola portal de Azure, debe instalar el componente de agente de diagnóstico de Hola para los recursos de servicios en la nube de Hola. Hello resto del tutorial de hello proporciona orientación sobre cómo tooinstall y configurar el agente de diagnóstico de hello tooenable el generador de perfiles de aplicación visión.

## <a name="prerequisites-for-hello-walkthrough"></a>Requisitos previos de tutorial Hola

* Una plantilla de administrador de recursos de implementación que instala agentes de generador de perfiles de hello en hello las máquinas virtuales ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) o conjuntos de escala ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).

* Una instancia de Application Insights habilitada para la generación de perfiles. Para obtener instrucciones, consulte [Habilitar perfil de hello](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).

* Recurso de servicios en la nube de destino de .NET framework 4.6.1 o posterior instalado en hello.

## <a name="create-a-resource-group-in-your-azure-subscription"></a>Creación de un grupo de recursos en la suscripción de Azure
Hola siguiente ejemplo muestra cómo agrupar toocreate un recurso mediante un script de PowerShell:

```
New-AzureRmResourceGroup -Name "Replace_With_Resource_Group_Name" -Location "Replace_With_Resource_Group_Location"
```

## <a name="create-an-application-insights-resource-in-hello-resource-group"></a>Crear un recurso de Application Insights en grupo de recursos de Hola
En hello **Application Insights** hoja, especifique la información de hello para el recurso, como se muestra en este ejemplo: 

![Hoja Application Insights](./media/enable-profiler-compute/createai.png)

## <a name="apply-an-application-insights-instrumentation-key-in-hello-azure-resource-manager-template"></a>Aplicar una clave de instrumentación de Application Insights en plantilla de Azure Resource Manager Hola

1. Si ha descargado todavía plantilla hello, descárguelo desde [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).

2. Encontrar la clave de Application Insights Hola.
   
   ![Ubicación de clave de Hola](./media/enable-profiler-compute/copyaikey.png)

3. Reemplace el valor de la plantilla de Hola.
   
   ![Valor reemplazado en la plantilla de Hola](./media/enable-profiler-compute/copyaikeytotemplate.png)

## <a name="create-an-azure-vm-toohost-hello-web-application"></a>Crear una aplicación web de Azure VM toohost Hola
1. Crear una contraseña de cadena segura toosave Hola.

   ```
   $password = ConvertTo-SecureString -String "Replace_With_Your_Password" -AsPlainText -Force
   ```

2. Implementar la plantilla de hello Azure Resource Manager.

   Cambie el directorio de hello en la carpeta toohello de consola de PowerShell de Hola que contiene la plantilla de administrador de recursos. plantilla de hello toodeploy, ejecute el siguiente comando de hello:

   ```
   New-AzureRmResourceGroupDeployment -ResourceGroupName "Replace_With_Resource_Group_Name" -TemplateFile .\WindowsVirtualMachine.json -adminUsername "Replace_With_your_user_name" -adminPassword $password -dnsNameForPublicIP "Replace_WIth_your_DNS_Name" -Verbose
   ```

Una vez ejecutada correctamente la secuencia de comandos de hello, debería encontrar una máquina virtual denominada **MyWindowsVM** en el grupo de recursos.

## <a name="configure-web-deploy-on-hello-vm"></a>Configurar Web Deploy en hello VM
Asegúrese de que Web Deploy esté habilitado en la máquina virtual de forma que pueda publicar la aplicación web desde Visual Studio.

tooinstall Web Deploy en una máquina virtual manualmente a través de WebPI, consulte [instalación y configuración de Web Deploy en IIS 8.0 o posterior](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later). Para obtener un ejemplo de cómo tooautomate instalar Web Deploy mediante una plantilla de Azure Resource Manager, consulte [crear, configurar e implementar una tooan de aplicación web VM de Azure](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).

Si va a implementar una aplicación ASP.NET MVC, vaya tooServer Manager, seleccione **agregar Roles y características** > **servidor Web (IIS)** > **Web Server**  >  **Desarrollo de aplicaciones**y habilitar ASP.NET 4.5 en el servidor.

![Adición de ASP.NET](./media/enable-profiler-compute/addaspnet45.png)

## <a name="install-hello-azure-application-insights-sdk-for-your-project"></a>Instalar hello Azure Application Insights SDK para el proyecto
1. Abra la aplicación web ASP.NET en Visual Studio.

2. Haga clic en proyecto de Hola y seleccione **agregar** > **servicios conectados**.

3. Seleccione **Application Insights**.

4. Siga las instrucciones de hello en página Hola. Seleccione el recurso de Application Insights de Hola que creó anteriormente.

5. Seleccione hello **registrar** botón.


## <a name="publish-hello-project-tooan-azure-vm"></a>Publicar Hola proyecto tooan máquina virtual de Azure
Hay toopublish de varias maneras de una máquina virtual de Azure tooan de aplicación. Una manera es toouse 2017 de Visual Studio.

1. Haga clic en proyecto de Hola y seleccione **publicar**.

2. Seleccione **máquinas virtuales de Microsoft Azure** como Hola publicar destino y siga los pasos de Hola.

   ![Publish-FromVS](./media/enable-profiler-compute/publishtoVM.png)

3. Ejecute una prueba de carga con la aplicación. Debería ver los resultados en la página Web portal de hello Application Insights instancia.


## <a name="enable-hello-profiler"></a>Habilitar el generador de perfiles de Hola
1. Vaya tooyour Application Insights **rendimiento** hoja y seleccione **configurar**.
   
   ![Icono Configurar](./media/enable-profiler-compute/enableprofiler1.png)
 
2. Seleccione **Habilitar el generador de perfiles**.
   
   ![Icono Habilitar el generador de perfiles](./media/enable-profiler-compute/enableprofiler2.png)

## <a name="add-a-performance-test-tooyour-application"></a>Agregar una aplicación de tooyour de prueba de rendimiento
Para poder recopilar algunos toobe de datos de ejemplo mostrado en el generador de perfiles de aplicación visión, siga estos pasos:

1. Examinar los recursos de Application Insights toohello que creó anteriormente. 

2. Vaya toohello **disponibilidad** hoja y agregue una prueba de rendimiento que envía la dirección URL de la aplicación de web solicitudes tooyour. 

   ![Adición de una prueba de rendimiento](./media/enable-profiler-compute/AvailabilityTest.png)

## <a name="view-your-performance-data"></a>Visualización de los datos de rendimiento

1. Espere 10 y 15 minutos para toocollect del generador de perfiles de Hola y analizar datos de Hola. 

2. Vaya toohello **rendimiento** hoja en el recurso de Application Insights y la vista de rendimiento de la aplicación cuando está bajo carga.

   ![Visualización del rendimiento](./media/enable-profiler-compute/aiperformance.png)

3. Icono de SELECT hello en **ejemplos** tooopen hello **vista seguimiento** hoja.

   ![Abrir la hoja de la vista de seguimiento de Hola](./media/enable-profiler-compute/traceview.png)


## <a name="work-with-an-existing-template"></a>Uso de una plantilla existente

1. Busque la declaración del recurso Hola diagnósticos de Azure en la plantilla de implementación.
   
   Si no tiene una declaración, puede crear uno que es similar a la declaración de hello en el siguiente ejemplo de Hola. Puede actualizar la plantilla de Hola de hello [sitio Web del explorador de recursos de Azure](https://resources.azure.com).

2. Publicador de cambios de Hola de `Microsoft.Azure.Diagnostics` demasiado`AIP.Diagnostics.Test`.

3. Para `typeHandlerVersion`, utilice `0.0`.

4. Asegúrese de que `autoUpgradeMinorVersion` se establece demasiado`true`.

5. Agregar nueva hello `ApplicationInsightsProfiler` instancia receptor Hola `WadCfg` objeto de configuración, tal y como se muestra en el siguiente ejemplo de Hola:

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

## <a name="enable-hello-profiler-on-virtual-machine-scale-sets"></a>Habilitar el generador de perfiles de hello en conjuntos de escalas de máquina virtual
toosee cómo tooenable Hola profiler, descargar hello [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) plantilla. Hola mismos cambios en un recurso de extensión de diagnóstico de máquina virtual plantilla toohello para el conjunto de escalas de máquina virtual de Hola se aplican.

Asegúrese de que cada instancia en conjunto de escalas de Hola tiene toohello de acceso a internet. Hola generador de perfiles de agente, a continuación, puede enviar muestras de hello recopilan tooApplication visión para la presentación y análisis.

## <a name="enable-hello-profiler-on-service-fabric-applications"></a>Habilitar el generador de perfiles de hello en aplicaciones de Service Fabric
1. Hola aprovisionar Service Fabric clúster toohave hello Azure extensión de diagnósticos que instala Hola generador de perfiles de agente.

2. Instalar Hola Application Insights SDK en el proyecto de Hola y configurar clave de Application Insights Hola.

3. Agregar telemetría de tooinstrument de código de aplicación.

### <a name="provision-hello-service-fabric-cluster-toohave-hello-azure-diagnostics-extension-that-installs-hello-profiler-agent"></a>Aprovisionar Hola Service Fabric clúster toohave Hola extensión de diagnósticos de Azure que instala Hola generador de perfiles de agente
Un clúster de Service Fabric puede ser seguro o no seguro. Puede establecer una toobe de clúster de puerta de enlace no seguras por lo que no requiere un certificado para el acceso. Los clústeres que hospedan lógica y datos empresariales deben ser seguros. Puede habilitar el generador de perfiles de hello en clústeres de Service Fabric seguros y no seguras. En este tutorial usa un clúster no seguras como un ejemplo tooexplain los cambios que son necesarios tooenable Hola profiler. Puede aprovisionar un clúster segura Hola igual.

1. Descargue [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json). Al igual que hizo con las máquinas virtuales y los conjuntos de escalado de máquinas virtuales, sustituya `Application_Insights_Key` por la clave de Application Insights:

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

2. Implementar la plantilla de hello mediante un script de PowerShell:

   ```
   Login-AzureRmAccount
   New-AzureRmResourceGroup -Name [Your_Resource_Group_Name] -Location [Your_Resource_Group_Location] -Verbose -Force
   New-AzureRmResourceGroupDeployment -Name [Choose_An_Arbitrary_Name] -ResourceGroupName [Your_Resource_Group_Name] -TemplateFile [Path_To_Your_Template]

   ```

### <a name="install-hello-application-insights-sdk-in-hello-project-and-configure-hello-application-insights-key"></a>Instalar Hola Application Insights SDK en proyecto de Hola y configurar la clave de Application Insights Hola
Instalar Hola Application Insights SDK desde hello [paquete NuGet](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/). Asegúrese de instalar una versión estable, la 2.3 o posterior. 

Para más información sobre la configuración de Application Insights en los proyectos, consulte [Using Service Fabric with Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md) (Uso de Service Fabric con Application Insights).

### <a name="add-application-code-tooinstrument-telemetry"></a>Agregar telemetría de tooinstrument de código de aplicación
1. Para cualquier fragmento de código que desea que tooinstrument, agregar un elemento using instrucción alrededor de ella. 

   En el siguiente ejemplo de Hola Hola `RunAsync` método es hacer algún trabajo y Hola `telemetryClient` clase captura telemetría Hola después de iniciarse. evento de Hello requiere un nombre único a través de la aplicación hello.

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

2. Implementar el clúster de Service Fabric toohello de aplicación. Espere 10 minutos para toorun de aplicación Hola. Para obtener un mejor efecto, puede ejecutar una prueba de carga en la aplicación hello. Del portal de Application Insights vaya toohello **rendimiento** hoja y se deberían ver ejemplos de seguimientos de generación de perfiles.

<!---
Commenting out these sections for now
## Enable hello Profiler on Cloud Services applications
[TODO]
## Enable hello Profiler on classic Azure Virtual Machines
[TODO]
## Enable hello Profiler on on-premise servers
[TODO]
--->

## <a name="next-steps"></a>Pasos siguientes

- Encuentre ayuda con los problemas de Profiler en la sección de [solución de problemas](app-insights-profiler.md#troubleshooting).

- Obtenga más información sobre el analizador de hello en [el generador de perfiles de aplicación visión](app-insights-profiler.md).
