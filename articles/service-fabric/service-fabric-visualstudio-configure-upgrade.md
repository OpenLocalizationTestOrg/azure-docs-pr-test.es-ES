---
title: "actualización de hello aaaConfigure de una aplicación de Service Fabric | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconfigure Hola configuración para actualizar una aplicación de Service Fabric mediante Microsoft Visual Studio."
services: service-fabric
documentationcenter: na
author: mikkelhegn
manager: mfussell
editor: tglee
ms.assetid: 1757ba85-0b7b-4f16-8a23-2ddaa61c86c6
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/29/2017
ms.author: mikkelhegn
ms.openlocfilehash: 8ca50aa9d911f3c98f017490c8fe29011e8d80cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-upgrade-of-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="177da-103">Configurar la actualización de Hola de una aplicación de Service Fabric en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="177da-103">Configure hello upgrade of a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="177da-104">Visual Studio tools para Azure Service Fabric proporcionan compatibilidad con la actualización para la publicación toolocal o clústeres remotos.</span><span class="sxs-lookup"><span data-stu-id="177da-104">Visual Studio tools for Azure Service Fabric provide upgrade support for publishing toolocal or remote clusters.</span></span> <span data-ttu-id="177da-105">Hay tres escenarios en que desea tooupgrade la versión más reciente de tooa de aplicación en lugar de reemplazar la aplicación hello durante las pruebas y depuración:</span><span class="sxs-lookup"><span data-stu-id="177da-105">There are three scenarios in which you want tooupgrade your application tooa newer version instead of replacing hello application during testing and debugging:</span></span>

* <span data-ttu-id="177da-106">Datos de la aplicación no se perderán durante la actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="177da-106">Application data won't be lost during hello upgrade.</span></span>
* <span data-ttu-id="177da-107">Disponibilidad permanece alta, por lo que no habrá ninguna interrupción del servicio durante la actualización de hello, si no hay suficientes instancias de servicio que se extienden desde los dominios de actualización.</span><span class="sxs-lookup"><span data-stu-id="177da-107">Availability remains high so there won't be any service interruption during hello upgrade, if there are enough service instances spread across upgrade domains.</span></span>
* <span data-ttu-id="177da-108">Pueden ejecutarse las pruebas en una aplicación mientras se realiza la actualización.</span><span class="sxs-lookup"><span data-stu-id="177da-108">Tests can be run against an application while it's being upgraded.</span></span>

## <a name="parameters-needed-tooupgrade"></a><span data-ttu-id="177da-109">Parámetros necesitan tooupgrade</span><span class="sxs-lookup"><span data-stu-id="177da-109">Parameters needed tooupgrade</span></span>
<span data-ttu-id="177da-110">Puede elegir entre dos tipos de implementación: normal o actualización.</span><span class="sxs-lookup"><span data-stu-id="177da-110">You can choose from two types of deployment: regular or upgrade.</span></span> <span data-ttu-id="177da-111">Una implementación regular borra cualquier información de implementación anterior y los datos en el clúster de hello, mientras que una implementación de actualización conserva.</span><span class="sxs-lookup"><span data-stu-id="177da-111">A regular deployment erases any previous deployment information and data on hello cluster, while an upgrade deployment preserves it.</span></span> <span data-ttu-id="177da-112">Cuando se actualiza una aplicación de Service Fabric en Visual Studio, necesita tooprovide de parámetros de actualización de la aplicación y las directivas de comprobación de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="177da-112">When you upgrade a Service Fabric application in Visual Studio, you need tooprovide application upgrade parameters and health check policies.</span></span> <span data-ttu-id="177da-113">Actualización de la aplicación los parámetros ayudan a controlar actualización hello, mientras que las directivas de comprobación de mantenimiento determinan si la actualización de hello tuvo éxito.</span><span class="sxs-lookup"><span data-stu-id="177da-113">Application upgrade parameters help control hello upgrade, while health check policies determine whether hello upgrade was successful.</span></span> <span data-ttu-id="177da-114">Consulte [Actualización de la aplicación de Service Fabric: parámetros de actualización](service-fabric-application-upgrade-parameters.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="177da-114">See [Service Fabric application upgrade: upgrade parameters](service-fabric-application-upgrade-parameters.md) for more details.</span></span>

<span data-ttu-id="177da-115">Existen tres modos de actualización: *Monitored*, *UnmonitoredAuto* y *UnmonitoredManual*.</span><span class="sxs-lookup"><span data-stu-id="177da-115">There are three upgrade modes: *Monitored*, *UnmonitoredAuto*, and *UnmonitoredManual*.</span></span>

* <span data-ttu-id="177da-116">Una actualización de supervisión de automatiza la actualización de Hola y aplicación de comprobación de estado.</span><span class="sxs-lookup"><span data-stu-id="177da-116">A Monitored upgrade automates hello upgrade and application health check.</span></span>
* <span data-ttu-id="177da-117">Una actualización UnmonitoredAuto automatiza la actualización de hello, pero omite la comprobación de estado de aplicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="177da-117">An UnmonitoredAuto upgrade automates hello upgrade, but skips hello application health check.</span></span>
* <span data-ttu-id="177da-118">Al realizar una actualización de UnmonitoredManual, necesita toomanually actualizar cada dominio de actualización.</span><span class="sxs-lookup"><span data-stu-id="177da-118">When you do an UnmonitoredManual upgrade, you need toomanually upgrade each upgrade domain.</span></span>

<span data-ttu-id="177da-119">Cada modo de actualización requiere diferentes conjuntos de parámetros.</span><span class="sxs-lookup"><span data-stu-id="177da-119">Each upgrade mode requires different sets of parameters.</span></span> <span data-ttu-id="177da-120">Vea [parámetros de actualización de la aplicación](service-fabric-application-upgrade-parameters.md) toolearn más información acerca de las opciones de actualización disponibles Hola.</span><span class="sxs-lookup"><span data-stu-id="177da-120">See [Application upgrade parameters](service-fabric-application-upgrade-parameters.md) toolearn more about hello available upgrade options.</span></span>

## <a name="upgrade-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="177da-121">Actualización de la aplicación de Service Fabric en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="177da-121">Upgrade a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="177da-122">Si usas tooupgrade herramientas de Visual Studio Service Fabric Hola una aplicación de Service Fabric, puede especificar un toobe de proceso de publicar una actualización en lugar de una implementación regular marcando hello **actualizar la aplicación hello** comprobar cuadro.</span><span class="sxs-lookup"><span data-stu-id="177da-122">If you’re using hello Visual Studio Service Fabric tools tooupgrade a Service Fabric application, you can specify a publish process toobe an upgrade rather than a regular deployment by checking hello **Upgrade hello application** check box.</span></span>

### <a name="tooconfigure-hello-upgrade-parameters"></a><span data-ttu-id="177da-123">parámetros de actualización de hello tooconfigure</span><span class="sxs-lookup"><span data-stu-id="177da-123">tooconfigure hello upgrade parameters</span></span>
1. <span data-ttu-id="177da-124">Haga clic en hello **configuración** casilla de verificación toohello siguiente botón.</span><span class="sxs-lookup"><span data-stu-id="177da-124">Click hello **Settings** button next toohello check box.</span></span> <span data-ttu-id="177da-125">Hola **editar parámetros actualizar** aparece el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="177da-125">hello **Edit Upgrade Parameters** dialog box appears.</span></span> <span data-ttu-id="177da-126">Hola **editar parámetros actualizar** cuadro de diálogo admite modos de actualización de hello supervisado, UnmonitoredAuto y UnmonitoredManual.</span><span class="sxs-lookup"><span data-stu-id="177da-126">hello **Edit Upgrade Parameters** dialog box supports hello Monitored, UnmonitoredAuto, and UnmonitoredManual upgrade modes.</span></span>
2. <span data-ttu-id="177da-127">Seleccione modo de actualización de Hola que desee toouse y, a continuación, rellene cuadrícula de parámetros de Hola.</span><span class="sxs-lookup"><span data-stu-id="177da-127">Select hello upgrade mode that you want toouse and then fill out hello parameter grid.</span></span>

    <span data-ttu-id="177da-128">Cada parámetro tiene valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="177da-128">Each parameter has default values.</span></span> <span data-ttu-id="177da-129">parámetro opcional de Hola *DefaultServiceTypeHealthPolicy* toma una entrada de la tabla hash.</span><span class="sxs-lookup"><span data-stu-id="177da-129">hello optional parameter *DefaultServiceTypeHealthPolicy* takes a hash table input.</span></span> <span data-ttu-id="177da-130">Este es un ejemplo del formato de entrada de tabla de hash y Hola para *DefaultServiceTypeHealthPolicy*:</span><span class="sxs-lookup"><span data-stu-id="177da-130">Here’s an example of hello hash table input format for *DefaultServiceTypeHealthPolicy*:</span></span>

    ```
    @{ ConsiderWarningAsError = "false"; MaxPercentUnhealthyDeployedApplications = 0; MaxPercentUnhealthyServices = 0; MaxPercentUnhealthyPartitionsPerService = 0; MaxPercentUnhealthyReplicasPerPartition = 0 }
    ```

    <span data-ttu-id="177da-131">*ServiceTypeHealthPolicyMap* es otro parámetro opcional que toma una entrada de la tabla hash en hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="177da-131">*ServiceTypeHealthPolicyMap* is another optional parameter that takes a hash table input in hello following format:</span></span>

    ```    
    @ {"ServiceTypeName" : "MaxPercentUnhealthyPartitionsPerService,MaxPercentUnhealthyReplicasPerPartition,MaxPercentUnhealthyServices"}
    ```

    <span data-ttu-id="177da-132">Este es un ejemplo real:</span><span class="sxs-lookup"><span data-stu-id="177da-132">Here's a real-life example:</span></span>

    ```
    @{ "ServiceTypeName01" = "5,10,5"; "ServiceTypeName02" = "5,5,5" }
    ```
3. <span data-ttu-id="177da-133">Si selecciona el modo de actualización de UnmonitoredManual, debe iniciar una toocontinue de consola de PowerShell manualmente y finalizar el proceso de actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="177da-133">If you select UnmonitoredManual upgrade mode, you must manually start a PowerShell console toocontinue and finish hello upgrade process.</span></span> <span data-ttu-id="177da-134">Consulte demasiado[actualización de la aplicación de Service Fabric: temas avanzados](service-fabric-application-upgrade-advanced.md) toolearn manual cómo actualizar works.</span><span class="sxs-lookup"><span data-stu-id="177da-134">Refer too[Service Fabric application upgrade: advanced topics](service-fabric-application-upgrade-advanced.md) toolearn how manual upgrade works.</span></span>

## <a name="upgrade-an-application-by-using-powershell"></a><span data-ttu-id="177da-135">Actualización de una aplicación mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="177da-135">Upgrade an application by using PowerShell</span></span>
<span data-ttu-id="177da-136">Puede usar cmdlets de PowerShell tooupgrade una aplicación de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="177da-136">You can use PowerShell cmdlets tooupgrade a Service Fabric application.</span></span> <span data-ttu-id="177da-137">Consulte [Tutorial sobre la actualización de aplicaciones de Service Fabric](service-fabric-application-upgrade-tutorial.md) y [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx) para obtener información detallada.</span><span class="sxs-lookup"><span data-stu-id="177da-137">See [Service Fabric application upgrade tutorial](service-fabric-application-upgrade-tutorial.md) and [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx) for detailed information.</span></span>

## <a name="specify-a-health-check-policy-in-hello-application-manifest-file"></a><span data-ttu-id="177da-138">Especificar una directiva de comprobación de mantenimiento en el archivo de manifiesto de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="177da-138">Specify a health check policy in hello application manifest file</span></span>
<span data-ttu-id="177da-139">Cada servicio en una aplicación de Service Fabric puede tener sus propios parámetros de directiva de mantenimiento que reemplazar los valores predeterminados de Hola.</span><span class="sxs-lookup"><span data-stu-id="177da-139">Every service in a Service Fabric application can have its own health policy parameters that override hello default values.</span></span> <span data-ttu-id="177da-140">Puede proporcionar estos valores de parámetro en el archivo de manifiesto de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="177da-140">You can provide these parameter values in hello application manifest file.</span></span>

<span data-ttu-id="177da-141">Hello en el ejemplo siguiente se muestra cómo tooapply un único estado de la comprobación de directiva de cada servicio en el manifiesto de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="177da-141">hello following example shows how tooapply a unique health check policy for each service in hello application manifest.</span></span>

```xml
<Policies>
    <HealthPolicy ConsiderWarningAsError="false" MaxPercentUnhealthyDeployedApplications="20">
        <DefaultServiceTypeHealthPolicy MaxPercentUnhealthyServices="20"               
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />
        <ServiceTypeHealthPolicy ServiceTypeName="ServiceTypeName1"
                MaxPercentUnhealthyServices="20"
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />      
    </HealthPolicy>
</Policies>
```
## <a name="next-steps"></a><span data-ttu-id="177da-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="177da-142">Next steps</span></span>
<span data-ttu-id="177da-143">Para obtener más información acerca de cómo implementar una aplicación, vea [Implementación de una aplicación existente en Azure Service Fabric](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="177da-143">For more information about deploying an application, see [Deploy an existing application in Azure Service Fabric](service-fabric-deploy-existing-app.md).</span></span>