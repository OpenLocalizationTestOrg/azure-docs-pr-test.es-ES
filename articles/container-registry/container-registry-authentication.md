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
# <a name="authenticate-with-a-private-docker-container-registry"></a><span data-ttu-id="94342-103">Autenticación con un registro de contenedor privado de Docker</span><span class="sxs-lookup"><span data-stu-id="94342-103">Authenticate with a private Docker container registry</span></span>
<span data-ttu-id="94342-104">toowork con imágenes de contenedor en un registro de contenedor de Azure, inicie sesión con hello `docker login` comando.</span><span class="sxs-lookup"><span data-stu-id="94342-104">toowork with container images in an Azure container registry, you log in using hello `docker login` command.</span></span> <span data-ttu-id="94342-105">Puede iniciar una sesión utilizando una **[entidad de servicio de Azure Active Directory](../active-directory/active-directory-application-objects.md)** o una **cuenta de administrador** específica de registro.</span><span class="sxs-lookup"><span data-stu-id="94342-105">You can log in using either an **[Azure Active Directory service principal](../active-directory/active-directory-application-objects.md)** or a registry-specific **admin account**.</span></span> <span data-ttu-id="94342-106">Este artículo proporciona más detalles sobre estas identidades.</span><span class="sxs-lookup"><span data-stu-id="94342-106">This article provides more detail about these identities.</span></span>



## <a name="service-principal"></a><span data-ttu-id="94342-107">Entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="94342-107">Service principal</span></span>

<span data-ttu-id="94342-108">También puede [asignar una entidad de servicio](container-registry-get-started-azure-cli.md#assign-a-service-principal) tooyour registro y usarlo para la autenticación básica de Docker.</span><span class="sxs-lookup"><span data-stu-id="94342-108">You can [assign a service principal](container-registry-get-started-azure-cli.md#assign-a-service-principal) tooyour registry and use it for basic Docker authentication.</span></span> <span data-ttu-id="94342-109">Se recomienda el uso de una entidad de servicio para la mayoría de los escenarios.</span><span class="sxs-lookup"><span data-stu-id="94342-109">Using a service principal is recommended for most scenarios.</span></span> <span data-ttu-id="94342-110">Proporcionar Id. de aplicación de Hola y la contraseña de hello servicio principal toohello `docker login` de comandos, como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="94342-110">Provide hello app ID and password of hello service principal toohello `docker login` command, as shown in hello following example:</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="94342-111">Una vez iniciada la sesión, Docker almacena en caché las credenciales de hello, por lo que no tiene identificador de aplicación de hello tooremember.</span><span class="sxs-lookup"><span data-stu-id="94342-111">Once logged in, Docker caches hello credentials, so you don't need tooremember hello app ID.</span></span>

> [!TIP]
> <span data-ttu-id="94342-112">Si lo desea, puede volver a generar contraseña de Hola de una entidad de servicio mediante la ejecución de hello `az ad sp reset-credentials` comando.</span><span class="sxs-lookup"><span data-stu-id="94342-112">If you want, you can regenerate hello password of a service principal by running hello `az ad sp reset-credentials` command.</span></span>
>


<span data-ttu-id="94342-113">Permitir que las entidades de servicio [acceso basado en roles](../active-directory/role-based-access-control-configure.md) tooa registro.</span><span class="sxs-lookup"><span data-stu-id="94342-113">Service principals allow [role-based access](../active-directory/role-based-access-control-configure.md) tooa registry.</span></span> <span data-ttu-id="94342-114">Los roles disponibles son:</span><span class="sxs-lookup"><span data-stu-id="94342-114">Available roles are:</span></span>
  * <span data-ttu-id="94342-115">Lector (acceso de solo extracción).</span><span class="sxs-lookup"><span data-stu-id="94342-115">Reader (pull only access).</span></span>
  * <span data-ttu-id="94342-116">Colaborador (extracción e inserción).</span><span class="sxs-lookup"><span data-stu-id="94342-116">Contributor (pull and push).</span></span>
  * <span data-ttu-id="94342-117">Propietario (extracción, inserción y asignar roles a los usuarios tooother).</span><span class="sxs-lookup"><span data-stu-id="94342-117">Owner (pull, push, and assign roles tooother users).</span></span>

<span data-ttu-id="94342-118">El acceso anónimo no está disponible en los registros de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="94342-118">Anonymous access is not available on Azure Container Registries.</span></span> <span data-ttu-id="94342-119">Para imágenes públicas puede usar [Docker Hub](https://docs.docker.com/docker-hub/).</span><span class="sxs-lookup"><span data-stu-id="94342-119">For public images you can use [Docker Hub](https://docs.docker.com/docker-hub/).</span></span>

<span data-ttu-id="94342-120">Puede asignar varias entidades de seguridad de servicio del registro de tooa, lo que permite acceso toodefine para distintos usuarios o aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="94342-120">You can assign multiple service principals tooa registry, which allows you toodefine access for different users or applications.</span></span> <span data-ttu-id="94342-121">Entidades de servicio también habilitar la conectividad "sin periféricos" tooa en desarrollador o escenarios de DevOps como hello en los ejemplos siguientes:</span><span class="sxs-lookup"><span data-stu-id="94342-121">Service principals also enable "headless" connectivity tooa registry in developer or DevOps scenarios such as hello following examples:</span></span>

  * <span data-ttu-id="94342-122">Implementaciones de contenedor de un sistemas de tooorchestration del registro como controlador de dominio/OS, Docker Swarm y Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="94342-122">Container deployments from a registry tooorchestration systems including DC/OS, Docker Swarm and Kubernetes.</span></span> <span data-ttu-id="94342-123">Puede también extraer toorelated de registros de contenedor Servicios de Azure como [servicio de contenedor](../container-service/index.yml), [servicio de aplicaciones](../app-service/index.md), [lote](../batch/index.md), [Service Fabric](/azure/service-fabric/)y otros.</span><span class="sxs-lookup"><span data-stu-id="94342-123">You can also pull container registries toorelated Azure services such as [Container Service](../container-service/index.yml), [App Service](../app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/), and others.</span></span>

  * <span data-ttu-id="94342-124">Integraciones e implementaciones soluciones continua (por ejemplo, Visual Studio Team Services o Jenkins) que la creación de imágenes de contenedor e inserción tooa registro.</span><span class="sxs-lookup"><span data-stu-id="94342-124">Continuous integration and deployment solutions (such as Visual Studio Team Services or Jenkins) that build container images and push them tooa registry.</span></span>





## <a name="admin-account"></a><span data-ttu-id="94342-125">Cuenta de administrador</span><span class="sxs-lookup"><span data-stu-id="94342-125">Admin account</span></span>
<span data-ttu-id="94342-126">Con cada registro que se crea, se crea una cuenta de administrador automáticamente.</span><span class="sxs-lookup"><span data-stu-id="94342-126">With each registry you create, an admin account gets created automatically.</span></span> <span data-ttu-id="94342-127">De forma predeterminada está deshabilitada la cuenta de hello, pero puede habilitarla y administrar credenciales de hello, por ejemplo a través de hello [portal](container-registry-get-started-portal.md#manage-registry-settings) o mediante hello [comandos de CLI de Azure 2.0](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span><span class="sxs-lookup"><span data-stu-id="94342-127">By default hello account is disabled, but you can enable it and manage hello credentials, for example through hello [portal](container-registry-get-started-portal.md#manage-registry-settings) or using hello [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span></span> <span data-ttu-id="94342-128">A cada cuenta de administrador se le proporcionan dos contraseñas, y las dos se pueden regenerar.</span><span class="sxs-lookup"><span data-stu-id="94342-128">Each admin account is provided with two passwords, both of which can be regenerated.</span></span> <span data-ttu-id="94342-129">las contraseñas de dos de Hello permiten del registro de toomaintain conexiones toohello mediante una contraseña mientras regenera Hola otra contraseña.</span><span class="sxs-lookup"><span data-stu-id="94342-129">hello two passwords allow you toomaintain connections toohello registry by using one password while you regenerate hello other password.</span></span> <span data-ttu-id="94342-130">Si está habilitada la cuenta de hello, puede pasar el nombre de usuario de Hola y cualquier toohello de contraseña `docker login` comando de registro de toohello de autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="94342-130">If hello account is enabled, you can pass hello user name and either password toohello `docker login` command for basic authentication toohello registry.</span></span> <span data-ttu-id="94342-131">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="94342-131">For example:</span></span>

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

> [!IMPORTANT]
> <span data-ttu-id="94342-132">cuenta de administrador de Hello está diseñado para un registro de hello tooaccess de usuario único, principalmente con fines de prueba.</span><span class="sxs-lookup"><span data-stu-id="94342-132">hello admin account is designed for a single user tooaccess hello registry, mainly for test purposes.</span></span> <span data-ttu-id="94342-133">No se recomienda credenciales de cuenta de administrador de tooshare Hola entre otros usuarios.</span><span class="sxs-lookup"><span data-stu-id="94342-133">It is not recommended tooshare hello admin account credentials among other users.</span></span> <span data-ttu-id="94342-134">Todos los usuarios aparecen como un registro de toohello de usuario único.</span><span class="sxs-lookup"><span data-stu-id="94342-134">All users appear as a single user toohello registry.</span></span> <span data-ttu-id="94342-135">Cambiar o deshabilitar esta cuenta deshabilita el acceso de registro para todos los usuarios que utilizan las credenciales de Hola.</span><span class="sxs-lookup"><span data-stu-id="94342-135">Changing or disabling this account disables registry access for all users who use hello credentials.</span></span>
>


### <a name="next-steps"></a><span data-ttu-id="94342-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="94342-136">Next steps</span></span>
* <span data-ttu-id="94342-137">[Insertar la primera imagen con hello CLI de Docker](container-registry-get-started-docker-cli.md).</span><span class="sxs-lookup"><span data-stu-id="94342-137">[Push your first image using hello Docker CLI](container-registry-get-started-docker-cli.md).</span></span>
* <span data-ttu-id="94342-138">Para obtener más información acerca de la autenticación en la vista previa de registro de contenedor de hello, vea hello [entrada de blog](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span><span class="sxs-lookup"><span data-stu-id="94342-138">For more information about authentication in hello Container Registry preview, see hello [blog post](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span></span>
