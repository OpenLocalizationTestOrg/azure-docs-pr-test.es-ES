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
# <a name="manage-an-azure-service-fabric-application-by-using-azure-cli-20"></a>Administración de una aplicación de Azure Service Fabric mediante la CLI de Azure 2.0

Obtenga información acerca de cómo toocreate y eliminar aplicaciones que se ejecutan en un clúster de Azure Service Fabric.

## <a name="prerequisites"></a>Requisitos previos

* Instale la CLI de Azure 2.0. A continuación, seleccione su clúster de Service Fabric. Para más información, consulte [Service Fabric y CLI de Azure 2.0](service-fabric-azure-cli-2-0.md).

* Tener un tejido de servicio aplicación paquete listo toobe implementado. Para obtener más información acerca de cómo tooauthor y el paquete de una aplicación que conozca hello [modelo de aplicaciones de Service Fabric](service-fabric-application-model.md).

## <a name="overview"></a>Información general

toodeploy una nueva aplicación, siga estos pasos:

1. Cargar un almacén de imágenes de aplicación paquete toohello Service Fabric.
2. Aprovisione un tipo de aplicación.
3. Especifique y cree una aplicación.
4. Especifique y cree servicios.

tooremove una aplicación existente, siga estos pasos:

1. Eliminar aplicación hello.
2. Hola anule asociado tipo de aplicación.
3. Eliminar contenido de la tienda de hello imagen.

## <a name="deploy-a-new-application"></a>Implementación de una nueva aplicación

toodeploy una nueva aplicación Hola completa después de las tareas.

### <a name="upload-a-new-application-package-toohello-image-store"></a>Cargar un nuevo almacén de imágenes de toohello de paquetes de aplicación

Antes de crear una aplicación, cargue el almacén de imágenes de hello aplicación paquete toohello Service Fabric. 

Por ejemplo, si el paquete de aplicación es Hola `app_package_dir` directorio, Hola de uso después de directorio de hello tooupload de comandos:

```azurecli
az sf application upload --path ~/app_package_dir
```

Para los paquetes de aplicación de gran tamaño, puede especificar hello `--show-progress` opción progreso de Hola de toodisplay de carga de Hola.

### <a name="provision-hello-application-type"></a>Tipo de aplicación de provisión Hola

Cuando haya finalizado la carga de hello, aprovisionar la aplicación hello. aplicación de hello tooprovision, Hola de uso siguiente comando:

```azurecli
az sf application provision --application-type-build-path app_package_dir
```

Hola valor para `application-type-build-path` es Hola nombre del directorio de Hola donde cargar el paquete de aplicación.

### <a name="create-an-application-from-an-application-type"></a>Creación de una aplicación desde un tipo de aplicación

Una vez configurada la aplicación hello, use Hola después tooname de comando y crear la aplicación:

```azurecli
az sf application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

`app-name`es nombre hello que quiere toouse de instancia de la aplicación hello. Puede obtener parámetros adicionales de manifiesto de aplicación previamente aprovisionados de Hola.

nombre de la aplicación Hello debe comenzar con el prefijo de hello `fabric:/`.

### <a name="create-services-for-hello-new-application"></a>Crear servicios de aplicación nueva Hola

Después de haber creado una aplicación, crear servicios de aplicación hello. En el siguiente ejemplo de Hola, creamos un nuevo servicio sin estado de nuestra aplicación. Servicios de Hola que se pueden crear desde una aplicación que se definen en un manifiesto de servicio Hola aprovisionado previamente paquete de aplicación.

```azurecli
az sf service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a>Comprobación de implementación y el estado de la aplicación

tooverify que se implementaron correctamente una aplicación y el servicio, compruebe que el servicio y aplicación Hola aparecen:

```azurecli
az sf application list
az sf service list --application-list TestApp
```

tooverify que el servicio de hello es correcto, utilice la salud similares de hello tooretrieve comandos de servicio de Hola y aplicación hello:

```azurecli
az sf application health --application-id TestApp
az sf service health --service-id TestApp/TestSvc
```

Las aplicaciones y los servicios correctos tienen un valor `HealthState` de `Ok`.

## <a name="remove-an-existing-application"></a>Eliminación de una aplicación existente

tooremove una aplicación Hola completa después de las tareas.

### <a name="delete-hello-application"></a>Eliminar aplicación hello

aplicación de hello toodelete, Hola de uso siguiente comando:

```azurecli
az sf application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a>Deshacer el aprovisionamiento de tipo de aplicación Hola

Después de eliminar la aplicación hello, se puede deshacer el aprovisionamiento de tipo de aplicación Hola si ya no lo necesite. tipo de aplicación de hello toounprovision, Hola de uso siguiente comando:

```azurecli
az sf application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

debe coincidir con la versión de nombre y el tipo del tipo de Hola Hola nombre y la versión Hola previamente aprovisionados manifiesto de aplicación.

### <a name="delete-hello-application-package"></a>Eliminar paquete de aplicación Hola

Después de que deshizo el aprovisionamiento de tipo de aplicación Hola, puede eliminar paquete de aplicación Hola Hola almacén de imágenes si ya no lo necesite. La eliminación de paquetes de aplicación le ayuda a recuperar espacio en disco. 

paquete de aplicación toodelete Hola Hola del almacén de imágenes, Hola de uso siguiente comando:

```azurecli
az sf application package-delete --content-path app_package_dir
```

`content-path`debe ser el nombre de hello del directorio de Hola que ha cargado cuando se creó la aplicación hello.

## <a name="related-articles"></a>Artículos relacionados

* [Introducción a Service Fabric y la CLI de Azure 2.0](service-fabric-azure-cli-2-0.md)
* [Introducción a la CLI de XPlat de Service Fabric](service-fabric-azure-cli.md)
