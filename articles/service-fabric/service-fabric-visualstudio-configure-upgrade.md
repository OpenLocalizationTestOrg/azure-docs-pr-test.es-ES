---
title: "Configuración de la actualización de una aplicación de Service Fabric | Microsoft Docs"
description: "Obtenga información sobre cómo configurar los parámetros para la actualización de la aplicación de Service Fabric mediante Microsoft Visual Studio."
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
ms.openlocfilehash: 314b29a56e4651222822f40a116af97a7372ff2c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-upgrade-of-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="0856d-103">Configuración de la actualización de una aplicación de Service Fabric en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0856d-103">Configure the upgrade of a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="0856d-104">Las herramientas de Visual Studio para Azure Service Fabric proporcionan compatibilidad con la actualización para la publicación el clústeres locales o remotos.</span><span class="sxs-lookup"><span data-stu-id="0856d-104">Visual Studio tools for Azure Service Fabric provide upgrade support for publishing to local or remote clusters.</span></span> <span data-ttu-id="0856d-105">Hay tres escenarios en los que le convendría actualizar la aplicación a una versión más reciente en lugar de reemplazarla durante las pruebas y la depuración:</span><span class="sxs-lookup"><span data-stu-id="0856d-105">There are three scenarios in which you want to upgrade your application to a newer version instead of replacing the application during testing and debugging:</span></span>

* <span data-ttu-id="0856d-106">Los datos de la aplicación no se perderán durante la actualización.</span><span class="sxs-lookup"><span data-stu-id="0856d-106">Application data won't be lost during the upgrade.</span></span>
* <span data-ttu-id="0856d-107">La disponibilidad permanece alta, por lo que no habrá ninguna interrupción del servicio durante la actualización, si no hay suficientes instancias de servicio que se extienden entre los dominios de actualización.</span><span class="sxs-lookup"><span data-stu-id="0856d-107">Availability remains high so there won't be any service interruption during the upgrade, if there are enough service instances spread across upgrade domains.</span></span>
* <span data-ttu-id="0856d-108">Pueden ejecutarse las pruebas en una aplicación mientras se realiza la actualización.</span><span class="sxs-lookup"><span data-stu-id="0856d-108">Tests can be run against an application while it's being upgraded.</span></span>

## <a name="parameters-needed-to-upgrade"></a><span data-ttu-id="0856d-109">Parámetros necesarios para la actualización</span><span class="sxs-lookup"><span data-stu-id="0856d-109">Parameters needed to upgrade</span></span>
<span data-ttu-id="0856d-110">Puede elegir entre dos tipos de implementación: normal o actualización.</span><span class="sxs-lookup"><span data-stu-id="0856d-110">You can choose from two types of deployment: regular or upgrade.</span></span> <span data-ttu-id="0856d-111">Una implementación normal borra cualquier información de implementación anterior y los datos en el clúster, mientras que una implementación de actualización los conserva.</span><span class="sxs-lookup"><span data-stu-id="0856d-111">A regular deployment erases any previous deployment information and data on the cluster, while an upgrade deployment preserves it.</span></span> <span data-ttu-id="0856d-112">Cuando actualice una aplicación de Service Fabric en Visual Studio, deberá proporcionar directivas de comprobación de estado y parámetros de actualización de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0856d-112">When you upgrade a Service Fabric application in Visual Studio, you need to provide application upgrade parameters and health check policies.</span></span> <span data-ttu-id="0856d-113">Los parámetros de actualización de la aplicación ayudan a controlar la actualización, mientras que las directivas de comprobación de estado determinan si la actualización se realizó correctamente o no.</span><span class="sxs-lookup"><span data-stu-id="0856d-113">Application upgrade parameters help control the upgrade, while health check policies determine whether the upgrade was successful.</span></span> <span data-ttu-id="0856d-114">Consulte [Actualización de la aplicación de Service Fabric: parámetros de actualización](service-fabric-application-upgrade-parameters.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="0856d-114">See [Service Fabric application upgrade: upgrade parameters](service-fabric-application-upgrade-parameters.md) for more details.</span></span>

<span data-ttu-id="0856d-115">Existen tres modos de actualización: *Monitored*, *UnmonitoredAuto* y *UnmonitoredManual*.</span><span class="sxs-lookup"><span data-stu-id="0856d-115">There are three upgrade modes: *Monitored*, *UnmonitoredAuto*, and *UnmonitoredManual*.</span></span>

* <span data-ttu-id="0856d-116">Una actualización Monitored automatiza la actualización y la comprobación de estado de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0856d-116">A Monitored upgrade automates the upgrade and application health check.</span></span>
* <span data-ttu-id="0856d-117">Una actualización UnmonitoredAuto automatiza la actualización, pero omite la comprobación de estado de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0856d-117">An UnmonitoredAuto upgrade automates the upgrade, but skips the application health check.</span></span>
* <span data-ttu-id="0856d-118">Cuando realice una actualización UnmonitoredManual, deberá actualizar manualmente cada dominio de actualización.</span><span class="sxs-lookup"><span data-stu-id="0856d-118">When you do an UnmonitoredManual upgrade, you need to manually upgrade each upgrade domain.</span></span>

<span data-ttu-id="0856d-119">Cada modo de actualización requiere diferentes conjuntos de parámetros.</span><span class="sxs-lookup"><span data-stu-id="0856d-119">Each upgrade mode requires different sets of parameters.</span></span> <span data-ttu-id="0856d-120">Consulte [Parámetros de actualización de la aplicación](service-fabric-application-upgrade-parameters.md) para obtener más información sobre las opciones de actualización disponibles.</span><span class="sxs-lookup"><span data-stu-id="0856d-120">See [Application upgrade parameters](service-fabric-application-upgrade-parameters.md) to learn more about the available upgrade options.</span></span>

## <a name="upgrade-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="0856d-121">Actualización de la aplicación de Service Fabric en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0856d-121">Upgrade a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="0856d-122">Si usa las herramientas de Visual Studio Service Fabric para actualizar una aplicación de Service Fabric, puede especificar un proceso de publicación para que sea una actualización en lugar de una implementación normal si activa la casilla **Actualizar la aplicación** .</span><span class="sxs-lookup"><span data-stu-id="0856d-122">If you’re using the Visual Studio Service Fabric tools to upgrade a Service Fabric application, you can specify a publish process to be an upgrade rather than a regular deployment by checking the **Upgrade the application** check box.</span></span>

### <a name="to-configure-the-upgrade-parameters"></a><span data-ttu-id="0856d-123">Para configurar los parámetros de actualización</span><span class="sxs-lookup"><span data-stu-id="0856d-123">To configure the upgrade parameters</span></span>
1. <span data-ttu-id="0856d-124">Haga clic en el botón **Configuración** situado junto a la casilla.</span><span class="sxs-lookup"><span data-stu-id="0856d-124">Click the **Settings** button next to the check box.</span></span> <span data-ttu-id="0856d-125">Aparecerá el cuadro de diálogo **Edit Upgrade Parameters** .</span><span class="sxs-lookup"><span data-stu-id="0856d-125">The **Edit Upgrade Parameters** dialog box appears.</span></span> <span data-ttu-id="0856d-126">El cuadro de diálogo **Edit Upgrade Parameters** admite los modos de actualización Monitored, UnmonitoredAuto y UnmonitoredManual.</span><span class="sxs-lookup"><span data-stu-id="0856d-126">The **Edit Upgrade Parameters** dialog box supports the Monitored, UnmonitoredAuto, and UnmonitoredManual upgrade modes.</span></span>
2. <span data-ttu-id="0856d-127">Seleccione el modo de actualización que quiera usar y luego complete la cuadrícula de parámetros.</span><span class="sxs-lookup"><span data-stu-id="0856d-127">Select the upgrade mode that you want to use and then fill out the parameter grid.</span></span>

    <span data-ttu-id="0856d-128">Cada parámetro tiene valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="0856d-128">Each parameter has default values.</span></span> <span data-ttu-id="0856d-129">El parámetro *DefaultServiceTypeHealthPolicy* opcional toma una entrada de tabla hash.</span><span class="sxs-lookup"><span data-stu-id="0856d-129">The optional parameter *DefaultServiceTypeHealthPolicy* takes a hash table input.</span></span> <span data-ttu-id="0856d-130">Este es un ejemplo del formato de entrada de la tabla hash para *DefaultServiceTypeHealthPolicy*:</span><span class="sxs-lookup"><span data-stu-id="0856d-130">Here’s an example of the hash table input format for *DefaultServiceTypeHealthPolicy*:</span></span>

    ```
    @{ ConsiderWarningAsError = "false"; MaxPercentUnhealthyDeployedApplications = 0; MaxPercentUnhealthyServices = 0; MaxPercentUnhealthyPartitionsPerService = 0; MaxPercentUnhealthyReplicasPerPartition = 0 }
    ```

    <span data-ttu-id="0856d-131">*ServiceTypeHealthPolicyMap* es otro parámetro opcional que toma una entrada de tabla hash en el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="0856d-131">*ServiceTypeHealthPolicyMap* is another optional parameter that takes a hash table input in the following format:</span></span>

    ```    
    @ {"ServiceTypeName" : "MaxPercentUnhealthyPartitionsPerService,MaxPercentUnhealthyReplicasPerPartition,MaxPercentUnhealthyServices"}
    ```

    <span data-ttu-id="0856d-132">Este es un ejemplo real:</span><span class="sxs-lookup"><span data-stu-id="0856d-132">Here's a real-life example:</span></span>

    ```
    @{ "ServiceTypeName01" = "5,10,5"; "ServiceTypeName02" = "5,5,5" }
    ```
3. <span data-ttu-id="0856d-133">Si selecciona el modo de actualización UnmonitoredManual, tendrá que iniciar manualmente una consola de PowerShell para continuar y finalizar el proceso de actualización.</span><span class="sxs-lookup"><span data-stu-id="0856d-133">If you select UnmonitoredManual upgrade mode, you must manually start a PowerShell console to continue and finish the upgrade process.</span></span> <span data-ttu-id="0856d-134">Consulte [Actualización de la aplicación de Service Fabric: temas avanzados](service-fabric-application-upgrade-advanced.md) para ver cómo funciona la actualización manual.</span><span class="sxs-lookup"><span data-stu-id="0856d-134">Refer to [Service Fabric application upgrade: advanced topics](service-fabric-application-upgrade-advanced.md) to learn how manual upgrade works.</span></span>

## <a name="upgrade-an-application-by-using-powershell"></a><span data-ttu-id="0856d-135">Actualización de una aplicación mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="0856d-135">Upgrade an application by using PowerShell</span></span>
<span data-ttu-id="0856d-136">Puede usar cmdlets de PowerShell para actualizar una aplicación de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="0856d-136">You can use PowerShell cmdlets to upgrade a Service Fabric application.</span></span> <span data-ttu-id="0856d-137">Consulte [Tutorial sobre la actualización de aplicaciones de Service Fabric](service-fabric-application-upgrade-tutorial.md) y [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx) para obtener información detallada.</span><span class="sxs-lookup"><span data-stu-id="0856d-137">See [Service Fabric application upgrade tutorial](service-fabric-application-upgrade-tutorial.md) and [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx) for detailed information.</span></span>

## <a name="specify-a-health-check-policy-in-the-application-manifest-file"></a><span data-ttu-id="0856d-138">Especificación de una directiva de comprobación de estado en el archivo de manifiesto de aplicación</span><span class="sxs-lookup"><span data-stu-id="0856d-138">Specify a health check policy in the application manifest file</span></span>
<span data-ttu-id="0856d-139">Cada servicio en una aplicación de Service Fabric puede tener sus propios parámetros de directiva de estado que reemplazan a los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="0856d-139">Every service in a Service Fabric application can have its own health policy parameters that override the default values.</span></span> <span data-ttu-id="0856d-140">Puede proporcionar estos valores de parámetro en el archivo de manifiesto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="0856d-140">You can provide these parameter values in the application manifest file.</span></span>

<span data-ttu-id="0856d-141">El ejemplo siguiente muestra cómo aplicar una directiva de comprobación de estado única para cada servicio en el manifiesto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="0856d-141">The following example shows how to apply a unique health check policy for each service in the application manifest.</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="0856d-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0856d-142">Next steps</span></span>
<span data-ttu-id="0856d-143">Para obtener más información acerca de cómo implementar una aplicación, vea [Implementación de una aplicación existente en Azure Service Fabric](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="0856d-143">For more information about deploying an application, see [Deploy an existing application in Azure Service Fabric](service-fabric-deploy-existing-app.md).</span></span>