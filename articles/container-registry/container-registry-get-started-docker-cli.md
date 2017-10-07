---
title: aaaPush Docker imagen tooprivate del registro de Azure | Documentos de Microsoft
description: "Inserción y extracción de Docker del registro del contenedor privado de tooa de imágenes en Azure con hello CLI de Docker"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 64fbe43f-fdde-4c17-a39a-d04f2d6d90a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a81a6f4bfcb23642a89ac7631348d40e2f4911a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="push-your-first-image-tooa-private-docker-container-registry-using-hello-docker-cli"></a>Insertar el primera imagen tooa privada Docker contenedor registro mediante Hola CLI de Docker
Un registro de contenedor de Azure almacena y administra privado [Docker](http://hub.docker.com) imágenes del contenedor, toohello similar forma [Docker Hub](https://hub.docker.com/) almacena imágenes públicas de Docker. Usar hello [interfaz de línea de comandos de Docker](https://docs.docker.com/engine/reference/commandline/cli/) (CLI de Docker) para [inicio de sesión](https://docs.docker.com/engine/reference/commandline/login/), [inserción](https://docs.docker.com/engine/reference/commandline/push/), [extracción](https://docs.docker.com/engine/reference/commandline/pull/)y otras operaciones en el contenedor registro.

Para obtener más datos y conceptos, vea [Hola información general](container-registry-intro.md)



## <a name="prerequisites"></a>Requisitos previos
* **Registro de contenedor de Azure**: cree un registro de contenedor en la suscripción de Azure. Por ejemplo, usar hello [portal de Azure](container-registry-get-started-portal.md) o hello [CLI de Azure 2.0](container-registry-get-started-azure-cli.md).
* **CLI de docker** -tooset el equipo local como un host y el acceso Hola CLI de Docker comandos de Docker, instalar [motor de Docker](https://docs.docker.com/engine/installation/).

## <a name="log-in-tooa-registry"></a>Inicie sesión en el registro de tooa
Ejecutar `docker login` toolog en tooyour del registro de contenedor con su [las credenciales del registro](container-registry-authentication.md).

Hello en el ejemplo siguiente se pasa Hola ID y la contraseña de Azure Active Directory [entidad de servicio](../active-directory/active-directory-application-objects.md). Por ejemplo, que puede que haya asignado un registro de tooyour principal de servicio para un escenario de automatización.

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

> [!TIP]
> Asegúrese de nombre de registro completo de hello toospecify seguro (en minúsculas). En este ejemplo, es `myregistry.azurecr.io`.

## <a name="steps-toopull-and-push-an-image"></a>Pasos toopull e inserte una imagen
Hola seguir ejemplo descargas Hola Nginx imagen desde el registro de Docker Hub público hello, etiquetas para el registro de contenedor de Azure privada, lo inserta en el registro de tooyour, a continuación, se extrae de nuevo.

**1. Extraiga la imagen oficial de hello Docker para Nginx**

Primera extracción Hola pública Nginx imagen tooyour equipo local.

```
docker pull nginx
```
**2. Inicie el contenedor de hello Nginx**

Hello comando siguiente inicia contenedor Nginx local de hello interactivamente en el puerto 8080, permitiéndole salida toosee desde Nginx. Quita Hola ejecución una vez detenido el contenedor.

```
docker run -it --rm -p 8080:80 nginx
```

Examinar demasiado[http://localhost: 8080](http://localhost:8080) hello tooview ejecutando el contenedor. Verá un toohello similar de pantalla siguiente.

![Nginx en un equipo local](./media/container-registry-get-started-docker-cli/nginx.png)

toostop Hola contenedor en ejecución, pulse [CTRL] + [C].

**3. Crear un alias de imagen de hello en el registro**

Hello siguiente comando crea un alias de imagen de hello, con un registro de tooyour de ruta de acceso completa. Este ejemplo especifica hello `samples` desorden de tooavoid de espacio de nombres en la raíz de hello del registro de hello.

```
docker tag nginx myregistry.azurecr.io/samples/nginx
```  

**4. Registro de inserción Hola imágenes tooyour**

```
docker push myregistry.azurecr.io/samples/nginx
```

**5. Imagen de Hola de extracción desde el registro**

```
docker pull myregistry.azurecr.io/samples/nginx
```

**6. Inicie el contenedor de Nginx de Hola desde el registro**

```
docker run -it --rm -p 8080:80 myregistry.azurecr.io/samples/nginx
```

Examinar demasiado[http://localhost: 8080](http://localhost:8080) hello tooview ejecutando el contenedor.

toostop Hola contenedor en ejecución, pulse [CTRL] + [C].

**7. (Opcional) Quitar imagen Hola**

```
docker rmi myregistry.azurecr.io/samples/nginx
```

##<a name="concurrent-limits"></a>Límites simultáneos
En algunos escenarios, la ejecución de llamadas de forma simultánea podría producir errores. Hello en la tabla siguiente contiene los límites de Hola de llamadas concurrentes con operaciones de "Inserción" y "Pull" en el registro de contenedor de Azure:

| Operación  | Límite                                  |
| ---------- | -------------------------------------- |
| EXTRAER       | Seguridad too10 simultáneas extrae por registro |
| INSERTAR       | Seguridad too5 simultáneas inserta por registro |

## <a name="next-steps"></a>Pasos siguientes
Ahora que conoce los fundamentos de hello, ya está listo toostart mediante el registro. Por ejemplo, iniciar la implementación de contenedor imágenes tooan [servicio de contenedor de Azure](https://azure.microsoft.com/documentation/services/container-service/) clúster.
