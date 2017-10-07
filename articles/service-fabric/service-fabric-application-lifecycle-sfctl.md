---
title: aplicaciones de Azure Service Fabric aaaManage mediante la CLI de Azure Service Fabric
description: "Obtenga información acerca de cómo toodeploy y quitar aplicaciones de un servicio de Azure Fabric de clúster mediante el uso de CLI de Azure Service Fabric"
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: d9f98cee1d70f71a2aab68ff556956619910e4fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-service-fabric-cli"></a><span data-ttu-id="9cd6f-103">Administración de aplicaciones de Azure Service Fabric mediante la CLI de Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9cd6f-103">Manage an Azure Service Fabric application by using Azure Service Fabric CLI</span></span>

<span data-ttu-id="9cd6f-104">Obtenga información acerca de cómo toocreate y eliminar aplicaciones que se ejecutan en un clúster de Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-104">Learn how toocreate and delete applications that are running in an Azure Service Fabric cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9cd6f-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9cd6f-105">Prerequisites</span></span>

* <span data-ttu-id="9cd6f-106">Instale la CLI de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-106">Install Service Fabric CLI.</span></span> <span data-ttu-id="9cd6f-107">A continuación, seleccione su clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-107">Then, select your Service Fabric cluster.</span></span> <span data-ttu-id="9cd6f-108">Para más información, consulte [Introducción a la CLI de Service Fabric](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="9cd6f-108">For more information, see [Get started with Service Fabric CLI](service-fabric-cli.md).</span></span>

* <span data-ttu-id="9cd6f-109">Tener un tejido de servicio aplicación paquete listo toobe implementado.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-109">Have a Service Fabric application package ready toobe deployed.</span></span> <span data-ttu-id="9cd6f-110">Para obtener más información acerca de cómo tooauthor y el paquete de una aplicación que conozca hello [modelo de aplicaciones de Service Fabric](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="9cd6f-110">For more information about how tooauthor and package an application, read about hello [Service Fabric application model](service-fabric-application-model.md).</span></span>

## <a name="overview"></a><span data-ttu-id="9cd6f-111">Información general</span><span class="sxs-lookup"><span data-stu-id="9cd6f-111">Overview</span></span>

<span data-ttu-id="9cd6f-112">toodeploy una nueva aplicación, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="9cd6f-112">toodeploy a new application, complete these steps:</span></span>

1. <span data-ttu-id="9cd6f-113">Cargar un almacén de imágenes de aplicación paquete toohello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-113">Upload an application package toohello Service Fabric image store.</span></span>
2. <span data-ttu-id="9cd6f-114">Aprovisione un tipo de aplicación.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-114">Provision an application type.</span></span>
3. <span data-ttu-id="9cd6f-115">Especifique y cree una aplicación.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-115">Specify and create an application.</span></span>
4. <span data-ttu-id="9cd6f-116">Especifique y cree servicios.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-116">Specify and create services.</span></span>

<span data-ttu-id="9cd6f-117">tooremove una aplicación existente, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="9cd6f-117">tooremove an existing application, complete these steps:</span></span>

1. <span data-ttu-id="9cd6f-118">Eliminar aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-118">Delete hello application.</span></span>
2. <span data-ttu-id="9cd6f-119">Hola anule asociado tipo de aplicación.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-119">Unprovision hello associated application type.</span></span>
3. <span data-ttu-id="9cd6f-120">Eliminar contenido de la tienda de hello imagen.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-120">Delete hello image store content.</span></span>

## <a name="deploy-a-new-application"></a><span data-ttu-id="9cd6f-121">Implementación de una nueva aplicación</span><span class="sxs-lookup"><span data-stu-id="9cd6f-121">Deploy a new application</span></span>

<span data-ttu-id="9cd6f-122">toodeploy una nueva aplicación Hola completa después de tareas:</span><span class="sxs-lookup"><span data-stu-id="9cd6f-122">toodeploy a new application, complete hello following tasks:</span></span>

### <a name="upload-a-new-application-package-toohello-image-store"></a><span data-ttu-id="9cd6f-123">Cargar un nuevo almacén de imágenes de toohello de paquetes de aplicación</span><span class="sxs-lookup"><span data-stu-id="9cd6f-123">Upload a new application package toohello image store</span></span>

<span data-ttu-id="9cd6f-124">Antes de crear una aplicación, cargue el almacén de imágenes de hello aplicación paquete toohello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-124">Before you create an application, upload hello application package toohello Service Fabric image store.</span></span>

<span data-ttu-id="9cd6f-125">Por ejemplo, si el paquete de aplicación es Hola `app_package_dir` directorio, Hola de uso después de directorio de hello tooupload de comandos:</span><span class="sxs-lookup"><span data-stu-id="9cd6f-125">For example, if your application package is in hello `app_package_dir` directory, use hello following commands tooupload hello directory:</span></span>

```azurecli
sfctl application upload --path ~/app_package_dir
```

<span data-ttu-id="9cd6f-126">Para los paquetes de aplicación de gran tamaño, puede especificar hello `--show-progress` opción progreso de Hola de toodisplay de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-126">For large application packages, you can specify hello `--show-progress` option toodisplay hello progress of hello upload.</span></span>

### <a name="provision-hello-application-type"></a><span data-ttu-id="9cd6f-127">Tipo de aplicación de provisión Hola</span><span class="sxs-lookup"><span data-stu-id="9cd6f-127">Provision hello application type</span></span>

<span data-ttu-id="9cd6f-128">Cuando haya finalizado la carga de hello, aprovisionar la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-128">When hello upload is finished, provision hello application.</span></span> <span data-ttu-id="9cd6f-129">aplicación de hello tooprovision, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="9cd6f-129">tooprovision hello application, use hello following command:</span></span>

```azurecli
sfctl application provision --application-type-build-path app_package_dir
```

<span data-ttu-id="9cd6f-130">Hola valor para `application-type-build-path` es Hola nombre del directorio de Hola donde cargar el paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-130">hello value for `application-type-build-path` is hello name of hello directory where you uploaded your application package.</span></span>

### <a name="create-an-application-from-an-application-type"></a><span data-ttu-id="9cd6f-131">Creación de una aplicación desde un tipo de aplicación</span><span class="sxs-lookup"><span data-stu-id="9cd6f-131">Create an application from an application type</span></span>

<span data-ttu-id="9cd6f-132">Una vez configurada la aplicación hello, use Hola después tooname de comando y crear la aplicación:</span><span class="sxs-lookup"><span data-stu-id="9cd6f-132">After you provision hello application, use hello following command tooname and create your application:</span></span>

```azurecli
sfctl application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

<span data-ttu-id="9cd6f-133">`app-name`es nombre hello que quiere toouse de instancia de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-133">`app-name` is hello name that you want toouse for hello application instance.</span></span> <span data-ttu-id="9cd6f-134">Puede obtener parámetros adicionales del manifiesto de aplicación aprovisionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-134">You can get additional parameters from the previously provisioned application manifest.</span></span>

<span data-ttu-id="9cd6f-135">nombre de la aplicación Hello debe comenzar con el prefijo de hello `fabric:/`.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-135">hello application name must start with hello prefix `fabric:/`.</span></span>

### <a name="create-services-for-hello-new-application"></a><span data-ttu-id="9cd6f-136">Crear servicios de aplicación nueva Hola</span><span class="sxs-lookup"><span data-stu-id="9cd6f-136">Create services for hello new application</span></span>

<span data-ttu-id="9cd6f-137">Después de haber creado una aplicación, crear servicios de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-137">After you have created an application, create services from hello application.</span></span> <span data-ttu-id="9cd6f-138">En el siguiente ejemplo de Hola, creamos un nuevo servicio sin estado de nuestra aplicación.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-138">In hello following example, we create a new stateless service from our application.</span></span> <span data-ttu-id="9cd6f-139">Servicios de Hola que se pueden crear desde una aplicación que se definen en un manifiesto de servicio Hola aprovisionado previamente paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-139">hello services that you can create from an application are defined in a service manifest in hello previously provisioned application package.</span></span>

```azurecli
sfctl service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a><span data-ttu-id="9cd6f-140">Comprobación de implementación y el estado de la aplicación</span><span class="sxs-lookup"><span data-stu-id="9cd6f-140">Verify application deployment and health</span></span>

<span data-ttu-id="9cd6f-141">tooverify todo es correcto, utilice Hola siga los comandos de mantenimiento:</span><span class="sxs-lookup"><span data-stu-id="9cd6f-141">tooverify everything is healthy, use hello following health commands:</span></span>

```azurecli
sfctl application list
sfctl service list --application-id TestApp
```

<span data-ttu-id="9cd6f-142">tooverify que el servicio de hello es correcto, utilice la salud similares de hello tooretrieve comandos del servicio de Hola y de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="9cd6f-142">tooverify that hello service is healthy, use similar commands tooretrieve hello health of both hello service and the application:</span></span>

```azurecli
sfctl application health --application-id TestApp
sfctl service health --service-id TestApp/TestSvc
```

<span data-ttu-id="9cd6f-143">Las aplicaciones y los servicios correctos tienen un valor `HealthState` de `Ok`.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-143">Healthy services and applications have a `HealthState` value of `Ok`.</span></span>

## <a name="remove-an-existing-application"></a><span data-ttu-id="9cd6f-144">Eliminación de una aplicación existente</span><span class="sxs-lookup"><span data-stu-id="9cd6f-144">Remove an existing application</span></span>

<span data-ttu-id="9cd6f-145">tooremove una aplicación Hola completa después de tareas:</span><span class="sxs-lookup"><span data-stu-id="9cd6f-145">tooremove an application, complete hello following tasks:</span></span>

### <a name="delete-hello-application"></a><span data-ttu-id="9cd6f-146">Eliminar aplicación hello</span><span class="sxs-lookup"><span data-stu-id="9cd6f-146">Delete hello application</span></span>

<span data-ttu-id="9cd6f-147">aplicación de hello toodelete, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="9cd6f-147">toodelete hello application, use hello following command:</span></span>

```azurecli
sfctl application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a><span data-ttu-id="9cd6f-148">Deshacer el aprovisionamiento de tipo de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="9cd6f-148">Unprovision hello application type</span></span>

<span data-ttu-id="9cd6f-149">Después de eliminar la aplicación hello, se puede deshacer el aprovisionamiento de tipo de aplicación Hola si ya no lo necesite.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-149">After you delete hello application, you can unprovision hello application type if you no longer need it.</span></span> <span data-ttu-id="9cd6f-150">tipo de aplicación de hello toounprovision, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="9cd6f-150">toounprovision hello application type, use hello following command:</span></span>

```azurecli
sfctl application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

<span data-ttu-id="9cd6f-151">debe coincidir con la versión de nombre y el tipo del tipo de Hola Hola nombre y la versión Hola previamente aprovisionados manifiesto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-151">hello type name and type version must match hello name and version in hello previously provisioned application manifest.</span></span>

### <a name="delete-hello-application-package"></a><span data-ttu-id="9cd6f-152">Eliminar paquete de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="9cd6f-152">Delete hello application package</span></span>

<span data-ttu-id="9cd6f-153">Después de que deshizo el aprovisionamiento de tipo de aplicación Hola, puede eliminar paquete de aplicación Hola Hola almacén de imágenes si ya no lo necesite.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-153">After you have unprovisioned hello application type, you can delete hello application package from hello image store if you no longer need it.</span></span> <span data-ttu-id="9cd6f-154">La eliminación de paquetes de aplicación le ayuda a recuperar espacio en disco.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-154">Deleting application packages helps reclaim disk space.</span></span> 

<span data-ttu-id="9cd6f-155">paquete de aplicación toodelete Hola Hola del almacén de imágenes, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="9cd6f-155">toodelete hello application package from hello image store, use hello following command:</span></span>

```azurecli
sfctl store delete --content-path app_package_dir
```

<span data-ttu-id="9cd6f-156">`content-path`debe ser el nombre de hello del directorio de Hola que ha cargado cuando se creó la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-156">`content-path` must be hello name of hello directory that you uploaded when you created hello application.</span></span>

## <a name="upgrade-application"></a><span data-ttu-id="9cd6f-157">Actualización de una aplicación</span><span class="sxs-lookup"><span data-stu-id="9cd6f-157">Upgrade application</span></span>

<span data-ttu-id="9cd6f-158">Después de crear la aplicación, puede repetir Hola el mismo conjunto de pasos tooprovision una segunda versión de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-158">After creating your application, you can repeat hello same set of steps tooprovision a second version of your application.</span></span> <span data-ttu-id="9cd6f-159">A continuación, con una actualización de la aplicación de Service Fabric puede realizar la transición de segunda versión de Hola de toorunning de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-159">Then, with a Service Fabric application upgrade you can transition toorunning hello second version of hello application.</span></span> <span data-ttu-id="9cd6f-160">Para obtener más información, consulte la documentación de hello en [las actualizaciones de aplicaciones de Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="9cd6f-160">For more information, see hello documentation on [Service Fabric application upgrades](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="9cd6f-161">tooperform una actualización, primer aprovisionar Hola próxima versión de la aplicación hello usando Hola mismos comandos que antes:</span><span class="sxs-lookup"><span data-stu-id="9cd6f-161">tooperform an upgrade, first provision hello next version of hello application using hello same commands as before:</span></span>

```azurecli
sfctl application upload --path ~/app_package_dir_2
sfctl application provision --application-type-build-path app_package_dir_2
```

<span data-ttu-id="9cd6f-162">Se recomienda, a continuación, tooperform una actualización automática supervisada, inicie Hola actualización ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="9cd6f-162">It is recommended then tooperform a monitored automatic upgrade, launch hello upgrade by running hello following command:</span></span>

```azurecli
sfctl application upgrade --app-id TestApp --app-version 2.0.0 --parameters "{\"test\":\"value\"}" --mode Monitored
```

<span data-ttu-id="9cd6f-163">Las actualizaciones reemplazan los parámetros existentes por el conjunto especificado.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-163">Upgrades override existing parameters with whatever set is specified.</span></span> <span data-ttu-id="9cd6f-164">Parámetros de la aplicación se deben pasar como comando de actualización de toohello argumentos, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-164">Application parameters should be passed as arguments toohello upgrade command, if necessary.</span></span> <span data-ttu-id="9cd6f-165">Los parámetros de la aplicación deben codificarse como objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-165">Application parameters should be encoded as a JSON object.</span></span>

<span data-ttu-id="9cd6f-166">tooretrieve cualquier parámetro especificado anteriormente, puede usar hello `sfctl application info` comando.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-166">tooretrieve any parameters previously specified, you can use hello `sfctl application info` command.</span></span>

<span data-ttu-id="9cd6f-167">Cuando una actualización de la aplicación está en curso, se puede recuperar el estado de hello mediante el `sfctl application upgrade-status` comando.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-167">When an application upgrade is in progress, hello status can be retrieved using the `sfctl application upgrade-status` command.</span></span>

<span data-ttu-id="9cd6f-168">Por último, si una actualización está en curso y debe toobe cancela, puede usar hello `sfctl application upgrade-rollback` tooroll volver Hola actualización.</span><span class="sxs-lookup"><span data-stu-id="9cd6f-168">Finally, if an upgrade is in progress and needs toobe canceled, you can use hello `sfctl application upgrade-rollback` tooroll back hello upgrade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9cd6f-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9cd6f-169">Next steps</span></span>

* [<span data-ttu-id="9cd6f-170">Conceptos básicos de la CLI de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9cd6f-170">Service Fabric CLI basics</span></span>](service-fabric-cli.md)
* [<span data-ttu-id="9cd6f-171">Introducción a Service Fabric con Linux</span><span class="sxs-lookup"><span data-stu-id="9cd6f-171">Getting started with Service Fabric on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="9cd6f-172">Inicio de una la actualización de una aplicación de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9cd6f-172">Launching a Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)
