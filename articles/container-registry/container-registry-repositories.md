---
title: repositorios de registro del contenedor de aaaAzure | Documentos de Microsoft
description: "¿Cómo toouse repositorios de registro de contenedor de Azure para las imágenes de Docker"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: cristyg
ms.openlocfilehash: 108622c565e41777fbb1fc9da9a01168abc7a7fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a>Repositorios de Azure Container Registry

Registro de contenedor de Azure permite imágenes del contenedor toostore en repositorios. Mediante el almacenamiento de imágenes en repositorios, puede tener grupos de imágenes (o versión de imágenes) en entornos aislados. Puede especificar estos repositorios cuando realice una inserción del registro de tooyour de imágenes.


## <a name="prerequisites"></a>Requisitos previos
* **Registro de contenedor de Azure**: cree un registro de contenedor en la suscripción de Azure. Por ejemplo, usar hello [portal de Azure](container-registry-get-started-portal.md) o hello [CLI de Azure 2.0](container-registry-get-started-azure-cli.md).
* **CLI de docker** -tooset el equipo local como un host y el acceso Hola CLI de Docker comandos de Docker, instalar [motor de Docker](https://docs.docker.com/engine/installation/).
* **Una imagen de extracción** : extraer una imagen de registro de Docker Hub público hello, etiquetarlo y empújelo tooyour registro. Para obtener instrucciones sobre cómo insertar y extraer imágenes, vea [registro privada de inserción Docker imágenes tooAzure](container-registry-get-started-docker-cli.md).


## <a name="viewing-repositories-in-hello-portal"></a>Ver los repositorios en hello Portal

Una vez que haya insertado el registro de contenedor de tooyour de imágenes, puede ver una lista de repositorios de hello hospedaje imágenes Hola Hola portal de Azure.

Si ha seguido los pasos de Hola Hola [registro privada de Docker Push imágenes tooAzure](container-registry-get-started-docker-cli.md) artículo, ahora debería tener una imagen de Nginx en el registro de contenedor. Como parte de las instrucciones de hello, debe especificar un espacio de nombres de imagen de Hola. En el ejemplo de Hola siguiente, el comando de hello inserta repositorio de hello NGinx imágenes toohello "ejemplos":

```
docker push myregistry.azurecr.io/samples/nginx
```
 Azure Container Registry es compatible con los espacios de nombres del repositorio de varios niveles. Esta característica permite toogroup las colecciones de aplicación específico de imágenes tooa relacionados o una colección de desarrollo de aplicaciones toospecific o los equipos operativos. tooread más información acerca de los repositorios de registros de contenedor, consulte [registros de contenedor de privado Docker en Azure](container-registry-intro.md).

repositorios de tooview Hola contenedor del registro:

1. Inicie sesión en toohello portal de Azure
2. En hello **registro de contenedor de Azure** hoja, registro de hello seleccione desea tooinspect
3. En la hoja de registro de hello, haga clic en **repositorios** toosee una lista de todos los repositorios de Hola y sus imágenes
4. (Opcional) Seleccione las etiquetas de una imagen específica toosee

![Repositorios de portal de Hola](./media/container-registry-repositories/container-registry-repositories.png)


## <a name="next-steps"></a>Pasos siguientes
Ahora que conoce los fundamentos de hello, ya está listo toostart mediante el registro. Por ejemplo, iniciar la implementación de contenedor imágenes tooan [servicio de contenedor de Azure](https://azure.microsoft.com/documentation/services/container-service/) clúster.
