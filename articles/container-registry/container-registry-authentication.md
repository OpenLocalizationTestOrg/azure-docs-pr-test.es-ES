---
title: aaaAuthenticate con un registro de contenedor de Azure | Documentos de Microsoft
description: "Cómo toolog en tooan del registro de contenedor de Azure con Azure Active Directory service principal o una cuenta de administrador"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 128a937a-766a-415b-b9fc-35a6c2f27417
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a0b0462e8432b2567689debca322e2426baa7fa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-a-private-docker-container-registry"></a>Autenticación con un registro de contenedor privado de Docker
toowork con imágenes de contenedor en un registro de contenedor de Azure, inicie sesión con hello `docker login` comando. Puede iniciar una sesión utilizando una **[entidad de servicio de Azure Active Directory](../active-directory/active-directory-application-objects.md)** o una **cuenta de administrador** específica de registro. Este artículo proporciona más detalles sobre estas identidades.



## <a name="service-principal"></a>Entidad de servicio

También puede [asignar una entidad de servicio](container-registry-get-started-azure-cli.md#assign-a-service-principal) tooyour registro y usarlo para la autenticación básica de Docker. Se recomienda el uso de una entidad de servicio para la mayoría de los escenarios. Proporcionar Id. de aplicación de Hola y la contraseña de hello servicio principal toohello `docker login` de comandos, como se muestra en el siguiente ejemplo de Hola:

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

Una vez iniciada la sesión, Docker almacena en caché las credenciales de hello, por lo que no tiene identificador de aplicación de hello tooremember.

> [!TIP]
> Si lo desea, puede volver a generar contraseña de Hola de una entidad de servicio mediante la ejecución de hello `az ad sp reset-credentials` comando.
>


Permitir que las entidades de servicio [acceso basado en roles](../active-directory/role-based-access-control-configure.md) tooa registro. Los roles disponibles son:
  * Lector (acceso de solo extracción).
  * Colaborador (extracción e inserción).
  * Propietario (extracción, inserción y asignar roles a los usuarios tooother).

El acceso anónimo no está disponible en los registros de contenedor de Azure. Para imágenes públicas puede usar [Docker Hub](https://docs.docker.com/docker-hub/).

Puede asignar varias entidades de seguridad de servicio del registro de tooa, lo que permite acceso toodefine para distintos usuarios o aplicaciones. Entidades de servicio también habilitar la conectividad "sin periféricos" tooa en desarrollador o escenarios de DevOps como hello en los ejemplos siguientes:

  * Implementaciones de contenedor de un sistemas de tooorchestration del registro como controlador de dominio/OS, Docker Swarm y Kubernetes. Puede también extraer toorelated de registros de contenedor Servicios de Azure como [servicio de contenedor](../container-service/index.yml), [servicio de aplicaciones](../app-service/index.md), [lote](../batch/index.md), [Service Fabric](/azure/service-fabric/)y otros.

  * Integraciones e implementaciones soluciones continua (por ejemplo, Visual Studio Team Services o Jenkins) que la creación de imágenes de contenedor e inserción tooa registro.





## <a name="admin-account"></a>Cuenta de administrador
Con cada registro que se crea, se crea una cuenta de administrador automáticamente. De forma predeterminada está deshabilitada la cuenta de hello, pero puede habilitarla y administrar credenciales de hello, por ejemplo a través de hello [portal](container-registry-get-started-portal.md#manage-registry-settings) o mediante hello [comandos de CLI de Azure 2.0](container-registry-get-started-azure-cli.md#manage-admin-credentials). A cada cuenta de administrador se le proporcionan dos contraseñas, y las dos se pueden regenerar. las contraseñas de dos de Hello permiten del registro de toomaintain conexiones toohello mediante una contraseña mientras regenera Hola otra contraseña. Si está habilitada la cuenta de hello, puede pasar el nombre de usuario de Hola y cualquier toohello de contraseña `docker login` comando de registro de toohello de autenticación básica. Por ejemplo:

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

> [!IMPORTANT]
> cuenta de administrador de Hello está diseñado para un registro de hello tooaccess de usuario único, principalmente con fines de prueba. No se recomienda credenciales de cuenta de administrador de tooshare Hola entre otros usuarios. Todos los usuarios aparecen como un registro de toohello de usuario único. Cambiar o deshabilitar esta cuenta deshabilita el acceso de registro para todos los usuarios que utilizan las credenciales de Hola.
>


### <a name="next-steps"></a>Pasos siguientes
* [Insertar la primera imagen con hello CLI de Docker](container-registry-get-started-docker-cli.md).
* Para obtener más información acerca de la autenticación en la vista previa de registro de contenedor de hello, vea hello [entrada de blog](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).
