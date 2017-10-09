---
title: "Temas de actualización de aplicación aaaAdvanced | Documentos de Microsoft"
description: "En este artículo se trata algunos temas avanzados pertenecen tooupgrading una aplicación de Service Fabric."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: e29585ff-e96f-46f4-a07f-6682bbe63281
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar;chackdan
ms.openlocfilehash: bdaf3db6209c574d39f57e0bf9951fad5ad1cbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-advanced-topics"></a><span data-ttu-id="ea20c-103">Actualización de la aplicación de Service Fabric: temas avanzados</span><span class="sxs-lookup"><span data-stu-id="ea20c-103">Service Fabric application upgrade: advanced topics</span></span>
## <a name="adding-or-removing-services-during-an-application-upgrade"></a><span data-ttu-id="ea20c-104">Adición o eliminación de servicios durante la actualización de una aplicación</span><span class="sxs-lookup"><span data-stu-id="ea20c-104">Adding or removing services during an application upgrade</span></span>
<span data-ttu-id="ea20c-105">Si un nuevo servicio se agrega tooan aplicación que ya está implementado y publicado como una actualización, nuevo servicio de hello es aplicación de agregado toohello implementado.</span><span class="sxs-lookup"><span data-stu-id="ea20c-105">If a new service is added tooan application that is already deployed, and published as an upgrade, hello new service is added toohello deployed application.</span></span>  <span data-ttu-id="ea20c-106">Esta actualización no afecta a ninguno de los servicios de Hola que ya formaban parte de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="ea20c-106">Such an upgrade does not affect any of hello services that were already part of hello application.</span></span> <span data-ttu-id="ea20c-107">Sin embargo, se debe iniciar una instancia de servicio de Hola que se agregó para toobe de servicio nuevo de hello active (con hello `New-ServiceFabricService` cmdlet).</span><span class="sxs-lookup"><span data-stu-id="ea20c-107">However, an instance of hello service that was added must be started for hello new service toobe active (using hello `New-ServiceFabricService` cmdlet).</span></span>

<span data-ttu-id="ea20c-108">También se pueden quitar servicios de una aplicación como parte de una actualización.</span><span class="sxs-lookup"><span data-stu-id="ea20c-108">Services can also be removed from an application as part of an upgrade.</span></span> <span data-ttu-id="ea20c-109">Sin embargo, se deben detener todas las instancias actuales del servicio de Hola se van a eliminar antes de continuar con la actualización de hello (con hello `Remove-ServiceFabricService` cmdlet).</span><span class="sxs-lookup"><span data-stu-id="ea20c-109">However, all current instances of hello to-be-deleted service must be stopped before proceeding with hello upgrade (using hello `Remove-ServiceFabricService` cmdlet).</span></span>

## <a name="manual-upgrade-mode"></a><span data-ttu-id="ea20c-110">Modo de actualización manual</span><span class="sxs-lookup"><span data-stu-id="ea20c-110">Manual upgrade mode</span></span>
> [!NOTE]
> <span data-ttu-id="ea20c-111">modo manual no supervisada de Hello debe considerarse solo para una actualización de errores o suspendida.</span><span class="sxs-lookup"><span data-stu-id="ea20c-111">hello unmonitored manual mode should be considered only for a failed or suspended upgrade.</span></span> <span data-ttu-id="ea20c-112">modo supervisado de Hello es Hola recomienda el modo de actualización para las aplicaciones de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ea20c-112">hello monitored mode is hello recommended upgrade mode for Service Fabric applications.</span></span>
>
>

<span data-ttu-id="ea20c-113">Azure Service Fabric proporciona varios modos de actualización de clústeres de desarrollo y producción de toosupport.</span><span class="sxs-lookup"><span data-stu-id="ea20c-113">Azure Service Fabric provides multiple upgrade modes toosupport development and production clusters.</span></span> <span data-ttu-id="ea20c-114">Las opciones de implementación elegidas pueden ser diferentes para distintos entornos.</span><span class="sxs-lookup"><span data-stu-id="ea20c-114">Deployment options chosen may be different for different environments.</span></span>

<span data-ttu-id="ea20c-115">Hola supervisado de actualización gradual de la aplicación es toouse de actualización más habitual de hello en el entorno de producción de hello.</span><span class="sxs-lookup"><span data-stu-id="ea20c-115">hello monitored rolling application upgrade is hello most typical upgrade toouse in hello production environment.</span></span> <span data-ttu-id="ea20c-116">Cuando actualiza Hola se especifica la directiva, Service Fabric garantiza que la aplicación hello es correcto para poder continuar con la actualización Hola.</span><span class="sxs-lookup"><span data-stu-id="ea20c-116">When hello upgrade policy is specified, Service Fabric ensures that hello application is healthy before hello upgrade proceeds.</span></span>

 <span data-ttu-id="ea20c-117">Administrador de la aplicación Hello sirve manual Hola gradual a modo de actualización de aplicación toohave control total sobre el progreso de la actualización Hola a través de hello distintos dominios de actualización.</span><span class="sxs-lookup"><span data-stu-id="ea20c-117">hello application administrator can use hello manual rolling application upgrade mode toohave total control over hello upgrade progress through hello various upgrade domains.</span></span> <span data-ttu-id="ea20c-118">Este modo es útil cuando se requiere una directiva de evaluación de estado personalizado o compleja, o qué está ocurriendo una actualización no convencional (por ejemplo, aplicación hello ya está en pérdida de datos).</span><span class="sxs-lookup"><span data-stu-id="ea20c-118">This mode is useful when a customized or complex health evaluation policy is required, or a non-conventional upgrade is happening (for example, hello application is already in data loss).</span></span>

<span data-ttu-id="ea20c-119">Por último, hello automatizadas actualización gradual de la aplicación es útil para el desarrollo o pruebas de entornos tooprovide ciclo de una iteración rápida durante el desarrollo del servicio.</span><span class="sxs-lookup"><span data-stu-id="ea20c-119">Finally, hello automated rolling application upgrade is useful for development or testing environments tooprovide a fast iteration cycle during service development.</span></span>

## <a name="change-toomanual-upgrade-mode"></a><span data-ttu-id="ea20c-120">Cambiar el modo de actualización toomanual</span><span class="sxs-lookup"><span data-stu-id="ea20c-120">Change toomanual upgrade mode</span></span>
<span data-ttu-id="ea20c-121">**Manual**--Detener actualización de la aplicación hello en Hola Hola UD y cambio actual Actualizar tooUnmonitored de modo Manual.</span><span class="sxs-lookup"><span data-stu-id="ea20c-121">**Manual**--Stop hello application upgrade at hello current UD and change hello upgrade mode tooUnmonitored Manual.</span></span> <span data-ttu-id="ea20c-122">Hello administrador necesita llamada toomanually **MoveNextApplicationUpgradeDomainAsync** tooproceed con hello, actualizar o activar una reversión si se inicia una nueva actualización.</span><span class="sxs-lookup"><span data-stu-id="ea20c-122">hello administrator needs toomanually call **MoveNextApplicationUpgradeDomainAsync** tooproceed with hello upgrade or trigger a rollback by initiating a new upgrade.</span></span> <span data-ttu-id="ea20c-123">Una vez que la actualización de hello entra en el modo Manual hello, permanece en modo Manual de hello hasta que se inicia una nueva actualización.</span><span class="sxs-lookup"><span data-stu-id="ea20c-123">Once hello upgrade enters into hello Manual mode, it stays in hello Manual mode until a new upgrade is initiated.</span></span> <span data-ttu-id="ea20c-124">Hola **GetApplicationUpgradeProgressAsync** comando devuelve tejido\_aplicación\_actualizar\_estado\_GRADUALES\_al día\_pendiente.</span><span class="sxs-lookup"><span data-stu-id="ea20c-124">hello **GetApplicationUpgradeProgressAsync** command returns FABRIC\_APPLICATION\_UPGRADE\_STATE\_ROLLING\_FORWARD\_PENDING.</span></span>

## <a name="upgrade-with-a-diff-package"></a><span data-ttu-id="ea20c-125">Actualización con un paquete de diferencias</span><span class="sxs-lookup"><span data-stu-id="ea20c-125">Upgrade with a diff package</span></span>
<span data-ttu-id="ea20c-126">Puede actualizarse una aplicación de Service Fabric mediante el aprovisionamiento de un paquete de aplicación completo y autocontenido.</span><span class="sxs-lookup"><span data-stu-id="ea20c-126">A Service Fabric application can be upgraded by provisioning with a full, self-contained application package.</span></span> <span data-ttu-id="ea20c-127">Una aplicación también puede actualizarse mediante un paquete de diferencias que contiene solo de los archivos de aplicación de hello actualizado, Hola actualiza el manifiesto de aplicación y los archivos de manifiesto de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea20c-127">An application can also be upgraded by using a diff package that contains only hello updated application files, hello updated application manifest, and hello service manifest files.</span></span>

<span data-ttu-id="ea20c-128">Un paquete completo de la aplicación contiene todos los Hola archivos necesarios toostart y ejecuta una aplicación de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ea20c-128">A full application package contains all hello files necessary toostart and run a Service Fabric application.</span></span> <span data-ttu-id="ea20c-129">Un paquete de diferencias contiene sólo los archivos de hello cambiado entre aprovisionar última Hola y de actualización actual de hello, además de manifiesto de aplicación completa de Hola y el servicio de hello los archivos de manifiesto.</span><span class="sxs-lookup"><span data-stu-id="ea20c-129">A diff package contains only hello files that changed between hello last provision and hello current upgrade, plus hello full application manifest and hello service manifest files.</span></span> <span data-ttu-id="ea20c-130">Cualquier referencia en el manifiesto de aplicación de Hola o manifiesto de servicio que no se encuentra en el diseño de la compilación de Hola se busca en el almacén de imágenes de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea20c-130">Any reference in hello application manifest or service manifest that can't be found in hello build layout is searched for in hello image store.</span></span>

<span data-ttu-id="ea20c-131">Paquetes de aplicación completo son necesarios para la primera instalación de un clúster de toohello de aplicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea20c-131">Full application packages are required for hello first installation of an application toohello cluster.</span></span> <span data-ttu-id="ea20c-132">Las actualizaciones posteriores pueden ser un paquete de aplicación completo o un paquete de diferencias.</span><span class="sxs-lookup"><span data-stu-id="ea20c-132">Subsequent updates can be either a full application package or a diff package.</span></span>

<span data-ttu-id="ea20c-133">Casos en los que usar un paquete de diferencias sería una buena opción:</span><span class="sxs-lookup"><span data-stu-id="ea20c-133">Occasions when using a diff package would be a good choice:</span></span>

* <span data-ttu-id="ea20c-134">Se prefiere un paquete de diferencias cuando tiene un paquete de aplicación grande que hace referencia a varios archivos del manifiesto de servicio o varios paquetes de código, configuración o datos.</span><span class="sxs-lookup"><span data-stu-id="ea20c-134">A diff package is preferred when you have a large application package that references several service manifest files and/or several code packages, config packages, or data packages.</span></span>
* <span data-ttu-id="ea20c-135">Un paquete de diferencias es preferible cuando tenga un sistema de implementación que se genera el diseño de la compilación de hello directamente desde el proceso de compilación de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ea20c-135">A diff package is preferred when you have a deployment system that generates hello build layout directly from your application build process.</span></span> <span data-ttu-id="ea20c-136">En este caso, incluso si no ha cambiado el código de hello, ensamblados recién creados obtienen una suma de comprobación diferentes.</span><span class="sxs-lookup"><span data-stu-id="ea20c-136">In this case, even though hello code hasn't changed, newly built assemblies get a different checksum.</span></span> <span data-ttu-id="ea20c-137">Uso de un paquete completo de la aplicación requeriría tooupdate Hola versión en todos los paquetes de código.</span><span class="sxs-lookup"><span data-stu-id="ea20c-137">Using a full application package would require you tooupdate hello version on all code packages.</span></span> <span data-ttu-id="ea20c-138">Con un paquete de diferencias, sólo proporcionar archivos Hola que ha cambiado y archivos de manifiesto de Hola que ha cambiado la versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea20c-138">Using a diff package, you only provide hello files that changed and hello manifest files where hello version has changed.</span></span>

<span data-ttu-id="ea20c-139">Cuando se actualiza una aplicación mediante Visual Studio, el paquete de diferencias de Hola se publica automáticamente.</span><span class="sxs-lookup"><span data-stu-id="ea20c-139">When an application is upgraded using Visual Studio, hello diff package is published automatically.</span></span> <span data-ttu-id="ea20c-140">toocreate un paquete de diferencias Hola manualmente, el manifiesto de aplicación y deben actualizarse los manifiestos de servicio de hello, pero solamente los paquetes de saludo cambiado deben incluirse en el paquete de aplicación final de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea20c-140">toocreate a diff package manually, hello application manifest, and hello service manifests must be updated, but only hello changed packages should be included in hello final application package.</span></span>

<span data-ttu-id="ea20c-141">Por ejemplo, puede empezar con hello tras la aplicación (números de versión proporcionados para facilitar la comprensión):</span><span class="sxs-lookup"><span data-stu-id="ea20c-141">For example, let's start with hello following application (version numbers provided for ease of understanding):</span></span>

```text
app1           1.0.0
  service1     1.0.0
    code       1.0.0
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

<span data-ttu-id="ea20c-142">Ahora, supongamos que desea tooupdate solo Hola paquete de código de service1 mediante un paquete de diferencias mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ea20c-142">Now, let's assume you wanted tooupdate only hello code package of service1 using a diff package using PowerShell.</span></span> <span data-ttu-id="ea20c-143">Ahora, la aplicación actualizada tiene Hola siguiendo la estructura de carpetas:</span><span class="sxs-lookup"><span data-stu-id="ea20c-143">Now, your updated application has hello following folder structure:</span></span>

```text
app1           2.0.0      <-- new version
  service1     2.0.0      <-- new version
    code       2.0.0      <-- new version
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

<span data-ttu-id="ea20c-144">En este caso, actualiza too2.0.0 de manifiesto de aplicación de Hola y el manifiesto de servicio de hello actualización del paquete de código de service1 tooreflect Hola.</span><span class="sxs-lookup"><span data-stu-id="ea20c-144">In this case, you update hello application manifest too2.0.0, and hello service manifest for service1 tooreflect hello code package update.</span></span> <span data-ttu-id="ea20c-145">carpeta de Hello para el paquete de aplicación tendría Hola siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="ea20c-145">hello folder for your application package would have hello following structure:</span></span>

```text
app1/
  service1/
    code/
```

## <a name="next-steps"></a><span data-ttu-id="ea20c-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ea20c-146">Next steps</span></span>
<span data-ttu-id="ea20c-147">[actualización de aplicaciones usando Visual Studio](service-fabric-application-upgrade-tutorial.md) ofrece información para actualizar una aplicación mediante Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ea20c-147">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="ea20c-148">[actualización de aplicaciones mediante PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) se explica en detalle lo que tiene que hacer para actualizar una aplicación mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ea20c-148">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="ea20c-149">Puede controlar cómo se actualiza una aplicación usando [parámetros de actualización](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="ea20c-149">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="ea20c-150">Hacer que las actualizaciones de la aplicación sea compatible por el aprendizaje cómo toouse [serialización de datos](service-fabric-application-upgrade-data-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="ea20c-150">Make your application upgrades compatible by learning how toouse [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="ea20c-151">Solucione problemas habituales en las actualizaciones de aplicaciones, se hace referencia a pasos toohello en [solución de problemas de las actualizaciones de aplicaciones](service-fabric-application-upgrade-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="ea20c-151">Fix common problems in application upgrades by referring toohello steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
