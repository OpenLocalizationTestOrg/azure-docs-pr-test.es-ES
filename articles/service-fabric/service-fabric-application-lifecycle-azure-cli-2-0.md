---
title: "Administración de aplicaciones de Azure Service Fabric mediante la CLI de Azure 2.0"
description: "Aprenda cómo implementar y quitar aplicaciones de un clúster de Azure Service Fabric mediante la CLI de Azure 2.0."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: 5728339236e3819b301e428f9d7a8add08f02b3e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-cli-20"></a><span data-ttu-id="cb416-103">Administración de una aplicación de Azure Service Fabric mediante la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="cb416-103">Manage an Azure Service Fabric application by using Azure CLI 2.0</span></span>

<span data-ttu-id="cb416-104">Aprenda cómo crear y eliminar aplicaciones que se ejecutan en un clúster de Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="cb416-104">Learn how to create and delete applications that are running in an Azure Service Fabric cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb416-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cb416-105">Prerequisites</span></span>

* <span data-ttu-id="cb416-106">Instale la CLI de Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="cb416-106">Install Azure CLI 2.0.</span></span> <span data-ttu-id="cb416-107">A continuación, seleccione su clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="cb416-107">Then, select your Service Fabric cluster.</span></span> <span data-ttu-id="cb416-108">Para más información, consulte [Service Fabric y CLI de Azure 2.0](service-fabric-azure-cli-2-0.md).</span><span class="sxs-lookup"><span data-stu-id="cb416-108">For more information, see [Get started with Azure CLI 2.0](service-fabric-azure-cli-2-0.md).</span></span>

* <span data-ttu-id="cb416-109">Tenga un paquete de aplicación de Service Fabric listo para la implementación.</span><span class="sxs-lookup"><span data-stu-id="cb416-109">Have a Service Fabric application package ready to be deployed.</span></span> <span data-ttu-id="cb416-110">Para más información sobre cómo crear y empaquetar una aplicación, lea la información sobre el [modelo de aplicación de Service Fabric](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="cb416-110">For more information about how to author and package an application, read about the [Service Fabric application model](service-fabric-application-model.md).</span></span>

## <a name="overview"></a><span data-ttu-id="cb416-111">Información general</span><span class="sxs-lookup"><span data-stu-id="cb416-111">Overview</span></span>

<span data-ttu-id="cb416-112">Para implementar una nueva aplicación, complete estos pasos:</span><span class="sxs-lookup"><span data-stu-id="cb416-112">To deploy a new application, complete these steps:</span></span>

1. <span data-ttu-id="cb416-113">Cargue un paquete de aplicación en el almacén de imágenes de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="cb416-113">Upload an application package to the Service Fabric image store.</span></span>
2. <span data-ttu-id="cb416-114">Aprovisione un tipo de aplicación.</span><span class="sxs-lookup"><span data-stu-id="cb416-114">Provision an application type.</span></span>
3. <span data-ttu-id="cb416-115">Especifique y cree una aplicación.</span><span class="sxs-lookup"><span data-stu-id="cb416-115">Specify and create an application.</span></span>
4. <span data-ttu-id="cb416-116">Especifique y cree servicios.</span><span class="sxs-lookup"><span data-stu-id="cb416-116">Specify and create services.</span></span>

<span data-ttu-id="cb416-117">Para quitar una aplicación existente, complete estos pasos:</span><span class="sxs-lookup"><span data-stu-id="cb416-117">To remove an existing application, complete these steps:</span></span>

1. <span data-ttu-id="cb416-118">Elimine la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cb416-118">Delete the application.</span></span>
2. <span data-ttu-id="cb416-119">Anule el aprovisionamiento del tipo de aplicación asociado.</span><span class="sxs-lookup"><span data-stu-id="cb416-119">Unprovision the associated application type.</span></span>
3. <span data-ttu-id="cb416-120">Elimine el contenido del almacén de imágenes.</span><span class="sxs-lookup"><span data-stu-id="cb416-120">Delete the image store content.</span></span>

## <a name="deploy-a-new-application"></a><span data-ttu-id="cb416-121">Implementación de una nueva aplicación</span><span class="sxs-lookup"><span data-stu-id="cb416-121">Deploy a new application</span></span>

<span data-ttu-id="cb416-122">Para implementar una nueva aplicación, complete las tareas siguientes.</span><span class="sxs-lookup"><span data-stu-id="cb416-122">To deploy a new application, complete the following tasks.</span></span>

### <a name="upload-a-new-application-package-to-the-image-store"></a><span data-ttu-id="cb416-123">Carga de un nuevo paquete de aplicación en el almacén de imágenes</span><span class="sxs-lookup"><span data-stu-id="cb416-123">Upload a new application package to the image store</span></span>

<span data-ttu-id="cb416-124">Antes de crear una aplicación, cargue el paquete de aplicación en el almacén de imágenes de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="cb416-124">Before you create an application, upload the application package to the Service Fabric image store.</span></span> 

<span data-ttu-id="cb416-125">Por ejemplo, si el paquete de aplicación está en el directorio `app_package_dir`, use los siguientes comandos para cargar el directorio:</span><span class="sxs-lookup"><span data-stu-id="cb416-125">For example, if your application package is in the `app_package_dir` directory, use the following commands to upload the directory:</span></span>

```azurecli
az sf application upload --path ~/app_package_dir
```

<span data-ttu-id="cb416-126">Para paquetes de aplicación de gran tamaño, puede especificar la opción `--show-progress` para mostrar el progreso de la carga.</span><span class="sxs-lookup"><span data-stu-id="cb416-126">For large application packages, you can specify the `--show-progress` option to display the progress of the upload.</span></span>

### <a name="provision-the-application-type"></a><span data-ttu-id="cb416-127">Aprovisionamiento del tipo de aplicación</span><span class="sxs-lookup"><span data-stu-id="cb416-127">Provision the application type</span></span>

<span data-ttu-id="cb416-128">Cuando la carga haya finalizado, aprovisione la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cb416-128">When the upload is finished, provision the application.</span></span> <span data-ttu-id="cb416-129">Utilice el siguiente comando para aprovisionar la aplicación:</span><span class="sxs-lookup"><span data-stu-id="cb416-129">To provision the application, use the following command:</span></span>

```azurecli
az sf application provision --application-type-build-path app_package_dir
```

<span data-ttu-id="cb416-130">El valor de `application-type-build-path` es el nombre del directorio donde cargó el paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="cb416-130">The value for `application-type-build-path` is the name of the directory where you uploaded your application package.</span></span>

### <a name="create-an-application-from-an-application-type"></a><span data-ttu-id="cb416-131">Creación de una aplicación desde un tipo de aplicación</span><span class="sxs-lookup"><span data-stu-id="cb416-131">Create an application from an application type</span></span>

<span data-ttu-id="cb416-132">Después de que se aprovisione la aplicación, utilice el comando siguiente para asignar un nombre a la aplicación y crearla:</span><span class="sxs-lookup"><span data-stu-id="cb416-132">After you provision the application, use the following command to name and create your application:</span></span>

```azurecli
az sf application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

<span data-ttu-id="cb416-133">`app-name` es el nombre que desea utilizar para la instancia de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cb416-133">`app-name` is the name that you want to use for the application instance.</span></span> <span data-ttu-id="cb416-134">Puede obtener parámetros adicionales del manifiesto de aplicación aprovisionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="cb416-134">You can get additional parameters from the previously provisioned application manifest.</span></span>

<span data-ttu-id="cb416-135">El nombre de la aplicación debe comenzar con el prefijo `fabric:/`.</span><span class="sxs-lookup"><span data-stu-id="cb416-135">The application name must start with the prefix `fabric:/`.</span></span>

### <a name="create-services-for-the-new-application"></a><span data-ttu-id="cb416-136">Creación de servicios para la nueva aplicación</span><span class="sxs-lookup"><span data-stu-id="cb416-136">Create services for the new application</span></span>

<span data-ttu-id="cb416-137">Una vez creada una aplicación, puede crear servicios desde ella.</span><span class="sxs-lookup"><span data-stu-id="cb416-137">After you have created an application, create services from the application.</span></span> <span data-ttu-id="cb416-138">En el siguiente ejemplo, creamos un nuevo servicio sin estado desde nuestra aplicación.</span><span class="sxs-lookup"><span data-stu-id="cb416-138">In the following example, we create a new stateless service from our application.</span></span> <span data-ttu-id="cb416-139">Los servicios que puede crear a partir de una aplicación se definen en un manifiesto de servicio en del paquete de aplicación aprovisionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="cb416-139">The services that you can create from an application are defined in a service manifest in the previously provisioned application package.</span></span>

```azurecli
az sf service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a><span data-ttu-id="cb416-140">Comprobación de implementación y el estado de la aplicación</span><span class="sxs-lookup"><span data-stu-id="cb416-140">Verify application deployment and health</span></span>

<span data-ttu-id="cb416-141">Para comprobar que una aplicación y un servicio se implementaron correctamente, compruebe que la aplicación y el servicio se muestren:</span><span class="sxs-lookup"><span data-stu-id="cb416-141">To verify that an application and service were successfully deployed, check that the application and service are listed:</span></span>

```azurecli
az sf application list
az sf service list --application-list TestApp
```

<span data-ttu-id="cb416-142">Para comprobar que el servicio es correcto, use comandos similares para recuperar tanto el estado del servicio como el de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="cb416-142">To verify that the service is healthy, use similar commands to retrieve the health of both the service and the application:</span></span>

```azurecli
az sf application health --application-id TestApp
az sf service health --service-id TestApp/TestSvc
```

<span data-ttu-id="cb416-143">Las aplicaciones y los servicios correctos tienen un valor `HealthState` de `Ok`.</span><span class="sxs-lookup"><span data-stu-id="cb416-143">Healthy services and applications have a `HealthState` value of `Ok`.</span></span>

## <a name="remove-an-existing-application"></a><span data-ttu-id="cb416-144">Eliminación de una aplicación existente</span><span class="sxs-lookup"><span data-stu-id="cb416-144">Remove an existing application</span></span>

<span data-ttu-id="cb416-145">Para quitar una nueva aplicación, complete las tareas siguientes.</span><span class="sxs-lookup"><span data-stu-id="cb416-145">To remove an application, complete the following tasks.</span></span>

### <a name="delete-the-application"></a><span data-ttu-id="cb416-146">Eliminación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="cb416-146">Delete the application</span></span>

<span data-ttu-id="cb416-147">Para eliminar la aplicación, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="cb416-147">To delete the application, use the following command:</span></span>

```azurecli
az sf application delete --application-id TestEdApp
```

### <a name="unprovision-the-application-type"></a><span data-ttu-id="cb416-148">Anulación del aprovisionamiento del tipo de aplicación</span><span class="sxs-lookup"><span data-stu-id="cb416-148">Unprovision the application type</span></span>

<span data-ttu-id="cb416-149">Después de eliminar la aplicación, puede deshacer el aprovisionamiento del tipo de aplicación si ya no lo necesita.</span><span class="sxs-lookup"><span data-stu-id="cb416-149">After you delete the application, you can unprovision the application type if you no longer need it.</span></span> <span data-ttu-id="cb416-150">Para anular el aprovisionamiento del tipo de aplicación, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="cb416-150">To unprovision the application type, use the following command:</span></span>

```azurecli
az sf application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

<span data-ttu-id="cb416-151">El nombre de tipo y la versión de tipo deben coincidir con el nombre y la versión del manifiesto de aplicación aprovisionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="cb416-151">The type name and type version must match the name and version in the previously provisioned application manifest.</span></span>

### <a name="delete-the-application-package"></a><span data-ttu-id="cb416-152">Eliminación del paquete de aplicación</span><span class="sxs-lookup"><span data-stu-id="cb416-152">Delete the application package</span></span>

<span data-ttu-id="cb416-153">Después de que se haya anulado el aprovisionamiento del tipo de aplicación, puede eliminar el paquete de aplicación del almacén de imágenes si ya no lo necesita.</span><span class="sxs-lookup"><span data-stu-id="cb416-153">After you have unprovisioned the application type, you can delete the application package from the image store if you no longer need it.</span></span> <span data-ttu-id="cb416-154">La eliminación de paquetes de aplicación le ayuda a recuperar espacio en disco.</span><span class="sxs-lookup"><span data-stu-id="cb416-154">Deleting application packages helps reclaim disk space.</span></span> 

<span data-ttu-id="cb416-155">Para eliminar el paquete de aplicación del almacén de imágenes, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="cb416-155">To delete the application package from the image store, use the following command:</span></span>

```azurecli
az sf application package-delete --content-path app_package_dir
```

<span data-ttu-id="cb416-156">`content-path` debe ser el nombre del directorio que cargó cuando creó la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cb416-156">`content-path` must be the name of the directory that you uploaded when you created the application.</span></span>

## <a name="related-articles"></a><span data-ttu-id="cb416-157">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="cb416-157">Related articles</span></span>

* [<span data-ttu-id="cb416-158">Introducción a Service Fabric y la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="cb416-158">Get started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
* [<span data-ttu-id="cb416-159">Introducción a la CLI de XPlat de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="cb416-159">Get started with Service Fabric XPlat CLI</span></span>](service-fabric-azure-cli.md)
