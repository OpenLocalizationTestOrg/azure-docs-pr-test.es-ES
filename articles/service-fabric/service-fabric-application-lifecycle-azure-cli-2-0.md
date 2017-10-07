---
title: aplicaciones de Azure Service Fabric aaaManage mediante Azure CLI 2.0
description: "Obtenga información acerca de cómo agrupar toodeploy y quitar aplicaciones de un tejido de servicio de Azure mediante Azure CLI 2.0."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ae1ba19513978b0f95ffb65d5f1f7a21ed5f2894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-cli-20"></a><span data-ttu-id="285fa-103">Administración de una aplicación de Azure Service Fabric mediante la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="285fa-103">Manage an Azure Service Fabric application by using Azure CLI 2.0</span></span>

<span data-ttu-id="285fa-104">Obtenga información acerca de cómo toocreate y eliminar aplicaciones que se ejecutan en un clúster de Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="285fa-104">Learn how toocreate and delete applications that are running in an Azure Service Fabric cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="285fa-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="285fa-105">Prerequisites</span></span>

* <span data-ttu-id="285fa-106">Instale la CLI de Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="285fa-106">Install Azure CLI 2.0.</span></span> <span data-ttu-id="285fa-107">A continuación, seleccione su clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="285fa-107">Then, select your Service Fabric cluster.</span></span> <span data-ttu-id="285fa-108">Para más información, consulte [Service Fabric y CLI de Azure 2.0](service-fabric-azure-cli-2-0.md).</span><span class="sxs-lookup"><span data-stu-id="285fa-108">For more information, see [Get started with Azure CLI 2.0](service-fabric-azure-cli-2-0.md).</span></span>

* <span data-ttu-id="285fa-109">Tener un tejido de servicio aplicación paquete listo toobe implementado.</span><span class="sxs-lookup"><span data-stu-id="285fa-109">Have a Service Fabric application package ready toobe deployed.</span></span> <span data-ttu-id="285fa-110">Para obtener más información acerca de cómo tooauthor y el paquete de una aplicación que conozca hello [modelo de aplicaciones de Service Fabric](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="285fa-110">For more information about how tooauthor and package an application, read about hello [Service Fabric application model](service-fabric-application-model.md).</span></span>

## <a name="overview"></a><span data-ttu-id="285fa-111">Información general</span><span class="sxs-lookup"><span data-stu-id="285fa-111">Overview</span></span>

<span data-ttu-id="285fa-112">toodeploy una nueva aplicación, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="285fa-112">toodeploy a new application, complete these steps:</span></span>

1. <span data-ttu-id="285fa-113">Cargar un almacén de imágenes de aplicación paquete toohello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="285fa-113">Upload an application package toohello Service Fabric image store.</span></span>
2. <span data-ttu-id="285fa-114">Aprovisione un tipo de aplicación.</span><span class="sxs-lookup"><span data-stu-id="285fa-114">Provision an application type.</span></span>
3. <span data-ttu-id="285fa-115">Especifique y cree una aplicación.</span><span class="sxs-lookup"><span data-stu-id="285fa-115">Specify and create an application.</span></span>
4. <span data-ttu-id="285fa-116">Especifique y cree servicios.</span><span class="sxs-lookup"><span data-stu-id="285fa-116">Specify and create services.</span></span>

<span data-ttu-id="285fa-117">tooremove una aplicación existente, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="285fa-117">tooremove an existing application, complete these steps:</span></span>

1. <span data-ttu-id="285fa-118">Eliminar aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="285fa-118">Delete hello application.</span></span>
2. <span data-ttu-id="285fa-119">Hola anule asociado tipo de aplicación.</span><span class="sxs-lookup"><span data-stu-id="285fa-119">Unprovision hello associated application type.</span></span>
3. <span data-ttu-id="285fa-120">Eliminar contenido de la tienda de hello imagen.</span><span class="sxs-lookup"><span data-stu-id="285fa-120">Delete hello image store content.</span></span>

## <a name="deploy-a-new-application"></a><span data-ttu-id="285fa-121">Implementación de una nueva aplicación</span><span class="sxs-lookup"><span data-stu-id="285fa-121">Deploy a new application</span></span>

<span data-ttu-id="285fa-122">toodeploy una nueva aplicación Hola completa después de las tareas.</span><span class="sxs-lookup"><span data-stu-id="285fa-122">toodeploy a new application, complete hello following tasks.</span></span>

### <a name="upload-a-new-application-package-toohello-image-store"></a><span data-ttu-id="285fa-123">Cargar un nuevo almacén de imágenes de toohello de paquetes de aplicación</span><span class="sxs-lookup"><span data-stu-id="285fa-123">Upload a new application package toohello image store</span></span>

<span data-ttu-id="285fa-124">Antes de crear una aplicación, cargue el almacén de imágenes de hello aplicación paquete toohello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="285fa-124">Before you create an application, upload hello application package toohello Service Fabric image store.</span></span> 

<span data-ttu-id="285fa-125">Por ejemplo, si el paquete de aplicación es Hola `app_package_dir` directorio, Hola de uso después de directorio de hello tooupload de comandos:</span><span class="sxs-lookup"><span data-stu-id="285fa-125">For example, if your application package is in hello `app_package_dir` directory, use hello following commands tooupload hello directory:</span></span>

```azurecli
az sf application upload --path ~/app_package_dir
```

<span data-ttu-id="285fa-126">Para los paquetes de aplicación de gran tamaño, puede especificar hello `--show-progress` opción progreso de Hola de toodisplay de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="285fa-126">For large application packages, you can specify hello `--show-progress` option toodisplay hello progress of hello upload.</span></span>

### <a name="provision-hello-application-type"></a><span data-ttu-id="285fa-127">Tipo de aplicación de provisión Hola</span><span class="sxs-lookup"><span data-stu-id="285fa-127">Provision hello application type</span></span>

<span data-ttu-id="285fa-128">Cuando haya finalizado la carga de hello, aprovisionar la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="285fa-128">When hello upload is finished, provision hello application.</span></span> <span data-ttu-id="285fa-129">aplicación de hello tooprovision, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="285fa-129">tooprovision hello application, use hello following command:</span></span>

```azurecli
az sf application provision --application-type-build-path app_package_dir
```

<span data-ttu-id="285fa-130">Hola valor para `application-type-build-path` es Hola nombre del directorio de Hola donde cargar el paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="285fa-130">hello value for `application-type-build-path` is hello name of hello directory where you uploaded your application package.</span></span>

### <a name="create-an-application-from-an-application-type"></a><span data-ttu-id="285fa-131">Creación de una aplicación desde un tipo de aplicación</span><span class="sxs-lookup"><span data-stu-id="285fa-131">Create an application from an application type</span></span>

<span data-ttu-id="285fa-132">Una vez configurada la aplicación hello, use Hola después tooname de comando y crear la aplicación:</span><span class="sxs-lookup"><span data-stu-id="285fa-132">After you provision hello application, use hello following command tooname and create your application:</span></span>

```azurecli
az sf application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

<span data-ttu-id="285fa-133">`app-name`es nombre hello que quiere toouse de instancia de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="285fa-133">`app-name` is hello name that you want toouse for hello application instance.</span></span> <span data-ttu-id="285fa-134">Puede obtener parámetros adicionales de manifiesto de aplicación previamente aprovisionados de Hola.</span><span class="sxs-lookup"><span data-stu-id="285fa-134">You can get additional parameters from hello previously provisioned application manifest.</span></span>

<span data-ttu-id="285fa-135">nombre de la aplicación Hello debe comenzar con el prefijo de hello `fabric:/`.</span><span class="sxs-lookup"><span data-stu-id="285fa-135">hello application name must start with hello prefix `fabric:/`.</span></span>

### <a name="create-services-for-hello-new-application"></a><span data-ttu-id="285fa-136">Crear servicios de aplicación nueva Hola</span><span class="sxs-lookup"><span data-stu-id="285fa-136">Create services for hello new application</span></span>

<span data-ttu-id="285fa-137">Después de haber creado una aplicación, crear servicios de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="285fa-137">After you have created an application, create services from hello application.</span></span> <span data-ttu-id="285fa-138">En el siguiente ejemplo de Hola, creamos un nuevo servicio sin estado de nuestra aplicación.</span><span class="sxs-lookup"><span data-stu-id="285fa-138">In hello following example, we create a new stateless service from our application.</span></span> <span data-ttu-id="285fa-139">Servicios de Hola que se pueden crear desde una aplicación que se definen en un manifiesto de servicio Hola aprovisionado previamente paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="285fa-139">hello services that you can create from an application are defined in a service manifest in hello previously provisioned application package.</span></span>

```azurecli
az sf service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a><span data-ttu-id="285fa-140">Comprobación de implementación y el estado de la aplicación</span><span class="sxs-lookup"><span data-stu-id="285fa-140">Verify application deployment and health</span></span>

<span data-ttu-id="285fa-141">tooverify que se implementaron correctamente una aplicación y el servicio, compruebe que el servicio y aplicación Hola aparecen:</span><span class="sxs-lookup"><span data-stu-id="285fa-141">tooverify that an application and service were successfully deployed, check that hello application and service are listed:</span></span>

```azurecli
az sf application list
az sf service list --application-list TestApp
```

<span data-ttu-id="285fa-142">tooverify que el servicio de hello es correcto, utilice la salud similares de hello tooretrieve comandos de servicio de Hola y aplicación hello:</span><span class="sxs-lookup"><span data-stu-id="285fa-142">tooverify that hello service is healthy, use similar commands tooretrieve hello health of both hello service and hello application:</span></span>

```azurecli
az sf application health --application-id TestApp
az sf service health --service-id TestApp/TestSvc
```

<span data-ttu-id="285fa-143">Las aplicaciones y los servicios correctos tienen un valor `HealthState` de `Ok`.</span><span class="sxs-lookup"><span data-stu-id="285fa-143">Healthy services and applications have a `HealthState` value of `Ok`.</span></span>

## <a name="remove-an-existing-application"></a><span data-ttu-id="285fa-144">Eliminación de una aplicación existente</span><span class="sxs-lookup"><span data-stu-id="285fa-144">Remove an existing application</span></span>

<span data-ttu-id="285fa-145">tooremove una aplicación Hola completa después de las tareas.</span><span class="sxs-lookup"><span data-stu-id="285fa-145">tooremove an application, complete hello following tasks.</span></span>

### <a name="delete-hello-application"></a><span data-ttu-id="285fa-146">Eliminar aplicación hello</span><span class="sxs-lookup"><span data-stu-id="285fa-146">Delete hello application</span></span>

<span data-ttu-id="285fa-147">aplicación de hello toodelete, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="285fa-147">toodelete hello application, use hello following command:</span></span>

```azurecli
az sf application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a><span data-ttu-id="285fa-148">Deshacer el aprovisionamiento de tipo de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="285fa-148">Unprovision hello application type</span></span>

<span data-ttu-id="285fa-149">Después de eliminar la aplicación hello, se puede deshacer el aprovisionamiento de tipo de aplicación Hola si ya no lo necesite.</span><span class="sxs-lookup"><span data-stu-id="285fa-149">After you delete hello application, you can unprovision hello application type if you no longer need it.</span></span> <span data-ttu-id="285fa-150">tipo de aplicación de hello toounprovision, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="285fa-150">toounprovision hello application type, use hello following command:</span></span>

```azurecli
az sf application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

<span data-ttu-id="285fa-151">debe coincidir con la versión de nombre y el tipo del tipo de Hola Hola nombre y la versión Hola previamente aprovisionados manifiesto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="285fa-151">hello type name and type version must match hello name and version in hello previously provisioned application manifest.</span></span>

### <a name="delete-hello-application-package"></a><span data-ttu-id="285fa-152">Eliminar paquete de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="285fa-152">Delete hello application package</span></span>

<span data-ttu-id="285fa-153">Después de que deshizo el aprovisionamiento de tipo de aplicación Hola, puede eliminar paquete de aplicación Hola Hola almacén de imágenes si ya no lo necesite.</span><span class="sxs-lookup"><span data-stu-id="285fa-153">After you have unprovisioned hello application type, you can delete hello application package from hello image store if you no longer need it.</span></span> <span data-ttu-id="285fa-154">La eliminación de paquetes de aplicación le ayuda a recuperar espacio en disco.</span><span class="sxs-lookup"><span data-stu-id="285fa-154">Deleting application packages helps reclaim disk space.</span></span> 

<span data-ttu-id="285fa-155">paquete de aplicación toodelete Hola Hola del almacén de imágenes, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="285fa-155">toodelete hello application package from hello image store, use hello following command:</span></span>

```azurecli
az sf application package-delete --content-path app_package_dir
```

<span data-ttu-id="285fa-156">`content-path`debe ser el nombre de hello del directorio de Hola que ha cargado cuando se creó la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="285fa-156">`content-path` must be hello name of hello directory that you uploaded when you created hello application.</span></span>

## <a name="related-articles"></a><span data-ttu-id="285fa-157">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="285fa-157">Related articles</span></span>

* [<span data-ttu-id="285fa-158">Introducción a Service Fabric y la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="285fa-158">Get started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
* [<span data-ttu-id="285fa-159">Introducción a la CLI de XPlat de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="285fa-159">Get started with Service Fabric XPlat CLI</span></span>](service-fabric-azure-cli.md)
