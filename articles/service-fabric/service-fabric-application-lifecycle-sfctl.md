---
title: "Administración de aplicaciones de Azure Service Fabric mediante la CLI de Azure Service Fabric"
description: "Aprenda a implementar y quitar aplicaciones de un clúster de Azure Service Fabric mediante la CLI de Azure Service Fabric."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: c3a2eb3e6e54f952ef963bb2a0292d9ad7b53bc5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-service-fabric-cli"></a><span data-ttu-id="85635-103">Administración de aplicaciones de Azure Service Fabric mediante la CLI de Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="85635-103">Manage an Azure Service Fabric application by using Azure Service Fabric CLI</span></span>

<span data-ttu-id="85635-104">Aprenda cómo crear y eliminar aplicaciones que se ejecutan en un clúster de Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="85635-104">Learn how to create and delete applications that are running in an Azure Service Fabric cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85635-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="85635-105">Prerequisites</span></span>

* <span data-ttu-id="85635-106">Instale la CLI de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="85635-106">Install Service Fabric CLI.</span></span> <span data-ttu-id="85635-107">A continuación, seleccione su clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="85635-107">Then, select your Service Fabric cluster.</span></span> <span data-ttu-id="85635-108">Para más información, consulte [Introducción a la CLI de Service Fabric](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="85635-108">For more information, see [Get started with Service Fabric CLI](service-fabric-cli.md).</span></span>

* <span data-ttu-id="85635-109">Tenga un paquete de aplicación de Service Fabric listo para la implementación.</span><span class="sxs-lookup"><span data-stu-id="85635-109">Have a Service Fabric application package ready to be deployed.</span></span> <span data-ttu-id="85635-110">Para más información sobre cómo crear y empaquetar una aplicación, lea la información sobre el [modelo de aplicación de Service Fabric](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="85635-110">For more information about how to author and package an application, read about the [Service Fabric application model](service-fabric-application-model.md).</span></span>

## <a name="overview"></a><span data-ttu-id="85635-111">Información general</span><span class="sxs-lookup"><span data-stu-id="85635-111">Overview</span></span>

<span data-ttu-id="85635-112">Para implementar una nueva aplicación, complete estos pasos:</span><span class="sxs-lookup"><span data-stu-id="85635-112">To deploy a new application, complete these steps:</span></span>

1. <span data-ttu-id="85635-113">Cargue un paquete de aplicación en el almacén de imágenes de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="85635-113">Upload an application package to the Service Fabric image store.</span></span>
2. <span data-ttu-id="85635-114">Aprovisione un tipo de aplicación.</span><span class="sxs-lookup"><span data-stu-id="85635-114">Provision an application type.</span></span>
3. <span data-ttu-id="85635-115">Especifique y cree una aplicación.</span><span class="sxs-lookup"><span data-stu-id="85635-115">Specify and create an application.</span></span>
4. <span data-ttu-id="85635-116">Especifique y cree servicios.</span><span class="sxs-lookup"><span data-stu-id="85635-116">Specify and create services.</span></span>

<span data-ttu-id="85635-117">Para quitar una aplicación existente, complete estos pasos:</span><span class="sxs-lookup"><span data-stu-id="85635-117">To remove an existing application, complete these steps:</span></span>

1. <span data-ttu-id="85635-118">Elimine la aplicación.</span><span class="sxs-lookup"><span data-stu-id="85635-118">Delete the application.</span></span>
2. <span data-ttu-id="85635-119">Anule el aprovisionamiento del tipo de aplicación asociado.</span><span class="sxs-lookup"><span data-stu-id="85635-119">Unprovision the associated application type.</span></span>
3. <span data-ttu-id="85635-120">Elimine el contenido del almacén de imágenes.</span><span class="sxs-lookup"><span data-stu-id="85635-120">Delete the image store content.</span></span>

## <a name="deploy-a-new-application"></a><span data-ttu-id="85635-121">Implementación de una nueva aplicación</span><span class="sxs-lookup"><span data-stu-id="85635-121">Deploy a new application</span></span>

<span data-ttu-id="85635-122">Para implementar una nueva aplicación, realice las tareas siguientes:</span><span class="sxs-lookup"><span data-stu-id="85635-122">To deploy a new application, complete the following tasks:</span></span>

### <a name="upload-a-new-application-package-to-the-image-store"></a><span data-ttu-id="85635-123">Carga de un nuevo paquete de aplicación en el almacén de imágenes</span><span class="sxs-lookup"><span data-stu-id="85635-123">Upload a new application package to the image store</span></span>

<span data-ttu-id="85635-124">Antes de crear una aplicación, cargue el paquete de aplicación en el almacén de imágenes de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="85635-124">Before you create an application, upload the application package to the Service Fabric image store.</span></span>

<span data-ttu-id="85635-125">Por ejemplo, si el paquete de aplicación está en el directorio `app_package_dir`, use los siguientes comandos para cargar el directorio:</span><span class="sxs-lookup"><span data-stu-id="85635-125">For example, if your application package is in the `app_package_dir` directory, use the following commands to upload the directory:</span></span>

```azurecli
sfctl application upload --path ~/app_package_dir
```

<span data-ttu-id="85635-126">Para paquetes de aplicación de gran tamaño, puede especificar la opción `--show-progress` para mostrar el progreso de la carga.</span><span class="sxs-lookup"><span data-stu-id="85635-126">For large application packages, you can specify the `--show-progress` option to display the progress of the upload.</span></span>

### <a name="provision-the-application-type"></a><span data-ttu-id="85635-127">Aprovisionamiento del tipo de aplicación</span><span class="sxs-lookup"><span data-stu-id="85635-127">Provision the application type</span></span>

<span data-ttu-id="85635-128">Cuando la carga haya finalizado, aprovisione la aplicación.</span><span class="sxs-lookup"><span data-stu-id="85635-128">When the upload is finished, provision the application.</span></span> <span data-ttu-id="85635-129">Utilice el siguiente comando para aprovisionar la aplicación:</span><span class="sxs-lookup"><span data-stu-id="85635-129">To provision the application, use the following command:</span></span>

```azurecli
sfctl application provision --application-type-build-path app_package_dir
```

<span data-ttu-id="85635-130">El valor de `application-type-build-path` es el nombre del directorio donde cargó el paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="85635-130">The value for `application-type-build-path` is the name of the directory where you uploaded your application package.</span></span>

### <a name="create-an-application-from-an-application-type"></a><span data-ttu-id="85635-131">Creación de una aplicación desde un tipo de aplicación</span><span class="sxs-lookup"><span data-stu-id="85635-131">Create an application from an application type</span></span>

<span data-ttu-id="85635-132">Después de que se aprovisione la aplicación, utilice el comando siguiente para asignar un nombre a la aplicación y crearla:</span><span class="sxs-lookup"><span data-stu-id="85635-132">After you provision the application, use the following command to name and create your application:</span></span>

```azurecli
sfctl application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

<span data-ttu-id="85635-133">`app-name` es el nombre que desea utilizar para la instancia de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="85635-133">`app-name` is the name that you want to use for the application instance.</span></span> <span data-ttu-id="85635-134">Puede obtener parámetros adicionales del manifiesto de aplicación aprovisionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="85635-134">You can get additional parameters from the previously provisioned application manifest.</span></span>

<span data-ttu-id="85635-135">El nombre de la aplicación debe comenzar con el prefijo `fabric:/`.</span><span class="sxs-lookup"><span data-stu-id="85635-135">The application name must start with the prefix `fabric:/`.</span></span>

### <a name="create-services-for-the-new-application"></a><span data-ttu-id="85635-136">Creación de servicios para la nueva aplicación</span><span class="sxs-lookup"><span data-stu-id="85635-136">Create services for the new application</span></span>

<span data-ttu-id="85635-137">Una vez creada una aplicación, puede crear servicios desde ella.</span><span class="sxs-lookup"><span data-stu-id="85635-137">After you have created an application, create services from the application.</span></span> <span data-ttu-id="85635-138">En el siguiente ejemplo, creamos un nuevo servicio sin estado desde nuestra aplicación.</span><span class="sxs-lookup"><span data-stu-id="85635-138">In the following example, we create a new stateless service from our application.</span></span> <span data-ttu-id="85635-139">Los servicios que puede crear a partir de una aplicación se definen en un manifiesto de servicio en del paquete de aplicación aprovisionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="85635-139">The services that you can create from an application are defined in a service manifest in the previously provisioned application package.</span></span>

```azurecli
sfctl service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a><span data-ttu-id="85635-140">Comprobación de implementación y el estado de la aplicación</span><span class="sxs-lookup"><span data-stu-id="85635-140">Verify application deployment and health</span></span>

<span data-ttu-id="85635-141">Para comprobar que todo es correcto, use los siguientes comandos de mantenimiento:</span><span class="sxs-lookup"><span data-stu-id="85635-141">To verify everything is healthy, use the following health commands:</span></span>

```azurecli
sfctl application list
sfctl service list --application-id TestApp
```

<span data-ttu-id="85635-142">Para comprobar que el servicio es correcto, use comandos similares para recuperar tanto el estado del servicio como el de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="85635-142">To verify that the service is healthy, use similar commands to retrieve the health of both the service and the application:</span></span>

```azurecli
sfctl application health --application-id TestApp
sfctl service health --service-id TestApp/TestSvc
```

<span data-ttu-id="85635-143">Las aplicaciones y los servicios correctos tienen un valor `HealthState` de `Ok`.</span><span class="sxs-lookup"><span data-stu-id="85635-143">Healthy services and applications have a `HealthState` value of `Ok`.</span></span>

## <a name="remove-an-existing-application"></a><span data-ttu-id="85635-144">Eliminación de una aplicación existente</span><span class="sxs-lookup"><span data-stu-id="85635-144">Remove an existing application</span></span>

<span data-ttu-id="85635-145">Para quitar una aplicación, realice las tareas siguientes:</span><span class="sxs-lookup"><span data-stu-id="85635-145">To remove an application, complete the following tasks:</span></span>

### <a name="delete-the-application"></a><span data-ttu-id="85635-146">Eliminación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="85635-146">Delete the application</span></span>

<span data-ttu-id="85635-147">Para eliminar la aplicación, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="85635-147">To delete the application, use the following command:</span></span>

```azurecli
sfctl application delete --application-id TestEdApp
```

### <a name="unprovision-the-application-type"></a><span data-ttu-id="85635-148">Anulación del aprovisionamiento del tipo de aplicación</span><span class="sxs-lookup"><span data-stu-id="85635-148">Unprovision the application type</span></span>

<span data-ttu-id="85635-149">Después de eliminar la aplicación, puede deshacer el aprovisionamiento del tipo de aplicación si ya no lo necesita.</span><span class="sxs-lookup"><span data-stu-id="85635-149">After you delete the application, you can unprovision the application type if you no longer need it.</span></span> <span data-ttu-id="85635-150">Para anular el aprovisionamiento del tipo de aplicación, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="85635-150">To unprovision the application type, use the following command:</span></span>

```azurecli
sfctl application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

<span data-ttu-id="85635-151">El nombre de tipo y la versión de tipo deben coincidir con el nombre y la versión del manifiesto de aplicación aprovisionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="85635-151">The type name and type version must match the name and version in the previously provisioned application manifest.</span></span>

### <a name="delete-the-application-package"></a><span data-ttu-id="85635-152">Eliminación del paquete de aplicación</span><span class="sxs-lookup"><span data-stu-id="85635-152">Delete the application package</span></span>

<span data-ttu-id="85635-153">Después de que se haya anulado el aprovisionamiento del tipo de aplicación, puede eliminar el paquete de aplicación del almacén de imágenes si ya no lo necesita.</span><span class="sxs-lookup"><span data-stu-id="85635-153">After you have unprovisioned the application type, you can delete the application package from the image store if you no longer need it.</span></span> <span data-ttu-id="85635-154">La eliminación de paquetes de aplicación le ayuda a recuperar espacio en disco.</span><span class="sxs-lookup"><span data-stu-id="85635-154">Deleting application packages helps reclaim disk space.</span></span> 

<span data-ttu-id="85635-155">Para eliminar el paquete de aplicación del almacén de imágenes, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="85635-155">To delete the application package from the image store, use the following command:</span></span>

```azurecli
sfctl store delete --content-path app_package_dir
```

<span data-ttu-id="85635-156">`content-path` debe ser el nombre del directorio que cargó cuando creó la aplicación.</span><span class="sxs-lookup"><span data-stu-id="85635-156">`content-path` must be the name of the directory that you uploaded when you created the application.</span></span>

## <a name="upgrade-application"></a><span data-ttu-id="85635-157">Actualización de una aplicación</span><span class="sxs-lookup"><span data-stu-id="85635-157">Upgrade application</span></span>

<span data-ttu-id="85635-158">Después de crear la aplicación, puede repetir el mismo conjunto de pasos para aprovisionar una segunda versión de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="85635-158">After creating your application, you can repeat the same set of steps to provision a second version of your application.</span></span> <span data-ttu-id="85635-159">Luego, con una actualización de la aplicación de Service Fabric puede pasar a la ejecución de la segunda versión de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="85635-159">Then, with a Service Fabric application upgrade you can transition to running the second version of the application.</span></span> <span data-ttu-id="85635-160">Para más información, consulte la documentación de [Actualización de la aplicación de Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="85635-160">For more information, see the documentation on [Service Fabric application upgrades](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="85635-161">Para llevar a cabo una actualización, primero aprovisione la siguiente versión de la aplicación mediante los mismos comandos que antes:</span><span class="sxs-lookup"><span data-stu-id="85635-161">To perform an upgrade, first provision the next version of the application using the same commands as before:</span></span>

```azurecli
sfctl application upload --path ~/app_package_dir_2
sfctl application provision --application-type-build-path app_package_dir_2
```

<span data-ttu-id="85635-162">Se recomienda luego realizar una actualización automática supervisada e iniciar la actualización ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="85635-162">It is recommended then to perform a monitored automatic upgrade, launch the upgrade by running the following command:</span></span>

```azurecli
sfctl application upgrade --app-id TestApp --app-version 2.0.0 --parameters "{\"test\":\"value\"}" --mode Monitored
```

<span data-ttu-id="85635-163">Las actualizaciones reemplazan los parámetros existentes por el conjunto especificado.</span><span class="sxs-lookup"><span data-stu-id="85635-163">Upgrades override existing parameters with whatever set is specified.</span></span> <span data-ttu-id="85635-164">Los parámetros de la aplicación se deben pasar como argumentos al comando de actualización, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="85635-164">Application parameters should be passed as arguments to the upgrade command, if necessary.</span></span> <span data-ttu-id="85635-165">Los parámetros de la aplicación deben codificarse como objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="85635-165">Application parameters should be encoded as a JSON object.</span></span>

<span data-ttu-id="85635-166">Para recuperar un parámetro anteriormente especificado, puede usar el comando `sfctl application info`.</span><span class="sxs-lookup"><span data-stu-id="85635-166">To retrieve any parameters previously specified, you can use the `sfctl application info` command.</span></span>

<span data-ttu-id="85635-167">Cuando una actualización de la aplicación está en curso, el estado se puede recuperar mediante el comando `sfctl application upgrade-status`.</span><span class="sxs-lookup"><span data-stu-id="85635-167">When an application upgrade is in progress, the status can be retrieved using the `sfctl application upgrade-status` command.</span></span>

<span data-ttu-id="85635-168">Finalmente, si una actualización está en curso y es necesario cancelarla, puede usar `sfctl application upgrade-rollback` para revertirla.</span><span class="sxs-lookup"><span data-stu-id="85635-168">Finally, if an upgrade is in progress and needs to be canceled, you can use the `sfctl application upgrade-rollback` to roll back the upgrade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="85635-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="85635-169">Next steps</span></span>

* [<span data-ttu-id="85635-170">Conceptos básicos de la CLI de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="85635-170">Service Fabric CLI basics</span></span>](service-fabric-cli.md)
* [<span data-ttu-id="85635-171">Introducción a Service Fabric con Linux</span><span class="sxs-lookup"><span data-stu-id="85635-171">Getting started with Service Fabric on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="85635-172">Inicio de una la actualización de una aplicación de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="85635-172">Launching a Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)
